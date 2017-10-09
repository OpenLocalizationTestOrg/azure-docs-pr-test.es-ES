---
title: "CENC con varios DRM y Access Control: diseño e implementación de referencia en Azure y Azure Media Services | Microsoft Docs"
description: "Obtenga información acerca de cómo toolicensing Hola Microsoft® Smooth Streaming Client Porting Kit."
services: media-services
documentationcenter: 
author: willzhan
manager: cfowler
editor: 
ms.assetid: 7814739b-cea9-4b9b-8370-538702e5c615
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: willzhan;kilroyh;yanmf;juliako
ms.openlocfilehash: 033fb618650c4fbe9069d467159a8734da759bba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="cenc-with-multi-drm-and-access-control-a-reference-design-and-implementation-on-azure-and-azure-media-services"></a>CENC con varios DRM y control de acceso: diseño e implementación de referencia en Azure y Servicios multimedia de Azure
 
## <a name="introduction"></a>Introducción
Es muy conocidos que es una tarea compleja toodesign y generar un subsistema DRM para un OTT o en pantalla de solución de transmisión por secuencias. Y es una práctica común para operadores/en línea toooutsource de proveedores de vídeo este proveedores de servicios de parte toospecialized DRM. objetivo de Hola de este documento es toopresent un diseño de referencia y la implementación de subsistema DRM-to-end de OTT o una solución de transmisión por secuencias en línea.

los lectores de Hello como destinada de este documento son ingenieros que trabajan en el subsistema DRM de OTT o soluciones en línea de transmisión por secuencias/multi-screen o cualquier lector interesado en el subsistema DRM. Hola, se supone que los lectores están familiarizados con al menos una de las tecnologías DRM de hello en el mercado de hello, como PlayReady, Widevine, FairPlay o acceso de Adobe.

En el término DRM, también incluimos CENC (Cifrado común) con varios DRM. Una tendencia principal en streaming en línea y sector OTT es toouse CENC con varios-native-DRM en varias plataformas de cliente, que es un cambio de tendencia anterior de hello del uso de un único DRM y el SDK de cliente para varias plataformas de cliente. Al utilizar CENC con varios native DRM, PlayReady y Widevine se cifran por hello [cifrado común (ISO/IEC 23001-7 CENC)](http://www.iso.org/iso/home/store/catalogue_ics/catalogue_detail_ics.htm?csnumber=65271/) especificación.

ventajas de Hola de CENC con DRM de múltiples son los siguientes:

1. Reduce el costo del cifrado puesto que se emplea un solo procesamiento de cifrado que tiene como destino distintas plataformas con sus DRM nativos.
2. Reduce el costo de Hola de administrar los recursos cifrados dado que no se necesita una sola copia de los recursos cifrados;
3. Elimina el costo de licencia porque Hola native client DRM es suele ser gratis en su plataforma nativa de cliente DRM.

Microsoft ha sido un promotor activo de DASH y CENC junto con algunos de los principales reproductores del sector. Servicios multimedia de Microsoft Azure ha estado ofreciendo soporte técnico para DASH y CENC. Para conocer los anuncios recientes, consulte los blogs de Mingfei: [Announcing Google Widevine license delivery services in Azure Media Services](https://azure.microsoft.com/blog/announcing-general-availability-of-google-widevine-license-services/) (Anuncio de los servicios de entrega de licencias de Google Widevine) y [Azure Media Services adds Google Widevine packaging for delivering multi-DRM stream](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/) (Azure Media Services agregan el paquete Google Widevine para la entrega de transmisiones de varios DRM).  

### <a name="overview-of-this-article"></a>Información general de este artículo
objetivo de Hola de este artículo incluye siguiente de hello:

1. Proporcionar un diseño de referencia del subsistema DRM mediante CENC con varios DRM.
2. Proporcionar una implementación de referencia en la plataforma de Servicios multimedia de Azure o Microsoft Azure.
3. Describir algunos temas de diseño e implementación.

En el artículo de hello, "multi-DRM" cubre siguiente hello:

1. Microsoft PlayReady
2. Google Widevine
3. Apple FairPlay 

Hello siguiente tabla resume aplicación nativa y plataforma nativa de hello y exploradores compatibles con cada DRM.

| **Plataforma de cliente** | **Compatibilidad con DRM nativo** | **Explorador/aplicación** | **Formatos de streaming** |
| --- | --- | --- | --- |
| **Televisores inteligentes, operador STB, OTT STB** |PlayReady principalmente o Widevine u otros |Linux, Opera y WebKit, otros |Varios formatos |
| **Dispositivos Windows 10 (Windows PC, tabletas de Windows, Windows Phone, Xbox)** |PlayReady |MS Edge/IE11/EME<br/><br/><br/>UWP |DASH (no se admite PlayReady para HLS)<br/><br/>DASH, Smooth Streaming (no se admite PlayReady para HLS) |
| **Dispositivos Android (teléfono, tableta, TV)** |Widevine |Chrome/EME |DASH, HLS |
| **iOS (iPhone, iPad), clientes de OS X y Apple TV** |FairPlay |Safari 8+/EME |HLS |


Teniendo en cuenta el estado actual de Hola de implementación para cada DRM, un servicio normalmente, deseará tooimplement 2 o 3 DRMs toomake seguro de que tratar todos los tipos de Hola de puntos de conexión de hello mejor manera.

Hay un equilibrio entre la complejidad de Hola de lógica de servicio de Hola y complejidad de hello en tooreach de lado de cliente de hello un cierto nivel de usuario de la experiencia en hello varios clientes.

toomake su selección, tenga en cuenta estos hechos:

* PlayReady se implementa de forma nativa en cada dispositivo de Windows, en algunos dispositivos Android y está disponibles a través de SDK de software en prácticamente cualquier plataforma.
* Widevine se implementa de forma nativa en todos los dispositivos Android, en Chrome y algunos otros dispositivos.
* FairPlay solo está disponible en clientes iOS y Mac OS o a través de iTunes.

Por tanto un multi-DRM típico sería:

* Opción 1: PlayReady y Widevine
* Opción 2: PlayReady, Widevine y FairPlay

## <a name="a-reference-design"></a>Un diseño de referencia
En esta sección, se presentará un diseño de referencia que es independiente tootechnologies utiliza tooimplement lo.

Un subsistema DRM puede contener Hola de los componentes siguientes:

1. Administración de claves
2. Empaquetado de DRM
3. Entrega de licencias DRM
4. Comprobación de derechos
5. Autenticación y autorización
6. Reproductor
7. Origen y CDN

Hello siguiente diagrama muestra hello alto nivel interacción entre los componentes de hello en un subsistema DRM.

![Subsistema DRM con CENC](./media/media-services-cenc-with-multidrm-access-control/media-services-generic-drm-subsystem-with-cenc.png)

Hay tres básicas "capas" en el diseño de hello:

1. Capa de área de operaciones (en negro), que no se expone externamente.
2. Capa de "Zona Desmilitarizada" (azul) que contiene todos los extremos de hello orientados al público;
3. Capa de Internet pública (azul claro), que contiene la CDN y los reproductores con el tráfico que atraviesa la Internet pública.

Debe haber una herramienta de administración del contenido para controlar la protección DRM, con independencia de que el cifrado sea estático o dinámico. deben incluir entradas de Hello para el cifrado de DRM:

1. Contenido de vídeo MBR
2. Clave de contenido
3. Las direcciones URL de adquisición de licencias.

Durante el tiempo de reproducción, flujo de nivel alto de hello es:

1. El usuario está autenticado.
2. Token de autorización se crea para el usuario de hello;
3. El contenido protegido con DRM (manifiesto) está descargado tooplayer;
4. El Reproductor envía servidores de toolicense de solicitud de adquisición de licencias junto con el identificador de clave y la autorización token.

Antes de mover toohello siguiente tema, algunas palabras sobre Hola de diseño de administración de claves.

| **Clave de contenido a activo** | **Escenario** |
| --- | --- |
| 1-1 |caso más simple de Hola. Proporciona mejor control posible Hola. Pero eso se suele traducir en el coste de entrega de licencia más elevado de Hola. Se requiere al menos una solicitud de licencia para cada activo protegido. |
| 1 a muchos |Puede usar Hola mismo contenido clave para varios activos. Por ejemplo, para todos los recursos de hello en un grupo lógico como un género o un subconjunto de género (o película Gene), podría utilizar una única clave de contenido. |
| Muchos a 1 |Se necesitan varias claves de contenido para cada activo. <br/><br/>Por ejemplo, si necesita tooapply dinámica CENC protección con DRM de múltiples de MPEG-DASH y cifrado de AES-128 dinámico para HLS, necesita dos claves de contenido independientes, cada uno con su propio ContentKeyType. (Hola clave de contenido utilizado para la protección de CENC dinámico, ContentKeyType.CommonEncryption debe usarse, mientras que para hello contenido se debe utilizar la clave utilizada para el cifrado AES-128 dinámico, ContentKeyType.EnvelopeEncryption.)<br/><br/>Otro ejemplo, en la protección de CENC de guión de contenido, en teoría, una clave de contenido puede ser usado tooprotect secuencia de vídeo y otra secuencia de audio tooprotect de clave de contenido. |
| Muchos – demasiado varios |Combinación de Hola por encima de los dos escenarios: Hola a un conjunto de contenido de las claves se utilizan para cada uno de varios activos en hello mismo "ID". |

Tooconsider de otro factor importante es el uso de Hola de licencias persistentes y no persistentes.

¿Por qué son importantes estas consideraciones?

Disponen de entrega de impacto directo toolicense costo si usas nube pública para la entrega de licencia. Veamos Hola siguiendo dos diseños casos tooillustrate:

1. Suscripción mensual: utiliza licencias persistentes y la asignación 1 a muchos entre claves de contenido y recursos. Por ejemplo, para todas las películas de niños hello, usamos una sola clave de contenido para el cifrado. En este caso:

    El número total de licencias solicitadas para todas las películas o dispositivos de niños = 1
2. Suscripción mensual: utiliza licencias no persistentes y asignación 1 a 1 entre claves de contenido y recursos. En este caso:

    El número total de licencias solicitadas para todas las películas o dispositivos de niños =  [n.º de películas vistas] x [n.º de sesiones].

Como puede ver fácilmente, Hola dos diseños diferentes como resultado licencia muy diferente solicitar patrones, por tanto, entrega de licencia de costo si no se proporciona el servicio de entrega de licencias por una nube pública, como los servicios multimedia de Azure.

## <a name="mapping-design-tootechnology-for-implementation"></a>Asignación tootechnology de diseño para la implementación
A continuación, se asigna el nuestro tootechnologies diseño genérico en la plataforma de servicios multimedia de Microsoft Azure o SQL Azure, mediante la especificación de qué toouse tecnología para cada bloque de creación.

Hello siguiente tabla muestra hello asignación:

| **Bloque de creación** | **Technology** |
| --- | --- |
| **Reproductor** |[Reproductor multimedia de Azure](https://azure.microsoft.com/services/media-services/media-player/) |
| **Proveedor de identidades (IDP)** |Azure Active Directory |
| **Servicio de token seguro (STS)** |Azure Active Directory |
| **Flujo de trabajo de protección DRM** |Protección dinámica de Servicios multimedia de Azure |
| **Entrega de licencias DRM** |1. Entrega de licencias de Azure Media Services (PlayReady, Widevine, FairPlay), o <br/>2. Servidor de licencias de Axinom, <br/>3. Servidor de licencias personalizado de PlayReady |
| **Origen** |Punto de conexión de streaming de Servicios multimedia de Azure |
| **Administración de claves** |No es necesaria para la implementación de referencia. |
| **Administración de contenido** |Una aplicación de consola de C#. |

En otras palabras, el proveedor de identidades (IDP) y el servicio de token seguro (STS) serán Azure AD. Para el reproductor, usaremos la [API del Reproductor multimedia de Azure](http://amp.azure.net/libs/amp/latest/docs/). Tanto los Servicios multimedia de Azure como el Reproductor multimedia de Azure admiten DASH y CENC con varios DRM.

Hola siguiente diagrama muestra Hola estructura y el flujo global con hello por encima de la asignación de tecnología.

![CENC en AMS](./media/media-services-cenc-with-multidrm-access-control/media-services-cenc-subsystem-on-AMS-platform.png)

En orden tooset el cifrado dinámico de CENC, herramienta de administración de contenido de hello usará Hola siguientes entradas:

1. Contenido abierto
2. Clave de contenido de la generación o administración de claves
3. Direcciones URL de adquisición de licencias
4. Una lista de información de Azure AD.

resultado de Hello de la herramienta de administración de contenido de hello será:

1. ContentKeyAuthorizationPolicy que contiene la especificación de hello en la entrega de licencias comprueba un token de JWT y especificaciones de licencias DRM;
2. AssetDeliveryPolicy, que contiene las especificaciones de formato de streaming, protección DRM y direcciones URL de adquisición de licencias.

En tiempo de ejecución, flujo de hello es como a continuación:

1. Tras la autenticación del usuario, se genera un token de JWT.
2. Una de las notificaciones de hello contenidas en el token de JWT de Hola es notificación "grupos" que contiene el identificador de objeto de grupo de Hola de "EntitledUserGroup". Esta notificación se utilizará para pasar la "comprobación de derechos".
3. Manifiesto de cliente de descargas de Reproductor de un CENC contenido protegido y "ve" siguiente hello:

   1. El id. de clave.
   2. contenido de Hello es CENC protegido,
   3. Las direcciones URL de adquisición de licencias.
4. El Reproductor realiza una solicitud de adquisición de licencias basada en Explorador de Hola/DRM admite. Símbolo (token) también se enviarán en solicitud de adquisición de licencias de hello, Id. de clave y de hello JWT. Servicio de entrega de licencia comprobará el token JWT de Hola y notificaciones de hello contenidas antes de emitir Hola necesita licencia.

## <a name="implementation"></a>Implementación
### <a name="implementation-procedures"></a>Procedimientos de implementación
implementación de Hello incluirá Hola pasos:

1. Preparar los recursos de prueba: fragmentado de codificar/paquete un vídeo de prueba toomulti-bitrate MP4 en servicios multimedia de Azure. Este activo NO está protegido con DRM. La protección DRM se realizará posteriormente mediante protección dinámica.
2. Crear el id. de clave y la clave de contenido (opcionalmente a partir de la inicialización de clave). Para nuestro propósito, el sistema de administración de claves no es necesario puesto que estamos trabajando con un solo conjunto de id. de clave y clave de contenido para un par de activos de prueba.
3. Usar servicios de entrega de licencia AMS API tooconfigure multi-DRM de los activos de prueba de Hola. Si usa servidores de licencias personalizados por su empresa o los proveedores de su empresa en lugar de servicios de licencias de servicios multimedia de Azure, puede omitir este paso y especifique las direcciones URL de adquisición de licencias en el paso de hello para la configuración de entrega de licencia. API de AMS es necesario toospecify detallada algunas configuraciones, como la restricción de la directiva de autorización, plantillas de respuesta de los servicios de licencias DRM diferentes, etcetera de licencia. En este momento, Hola portal de Azure proporcionan Hola necesita la interfaz de usuario para esta configuración, todavía no. Puede encontrar información de nivel de API y código de ejemplo en el documento de Julia Kornich: [Uso de cifrado dinámico común de PlayReady o Widevine](media-services-protect-with-drm.md).
4. Usar Directiva de entrega de API de AMS tooconfigure activo de los activos de prueba de Hola. Puede encontrar información de nivel de API y código de ejemplo en el documento de Julia Kornich: [Uso de cifrado dinámico común de PlayReady o Widevine](media-services-protect-with-drm.md).
5. Crear y configurar un inquilino de Azure Active Directory en Azure.
6. Crear algunas cuentas de usuario y grupos en su inquilino de Azure Active Directory: debe crear al menos "EntitledUser" agrupar y agregar un grupo de toothis de usuario. Los usuarios de este grupo pasará la comprobación de derechos en la adquisición de licencias y los usuarios de este grupo se producirá un error de comprobación de la autenticación de toopass y no se puede tooacquire ninguna licencia. Ser un miembro de este grupo de "EntitledUser" es una notificación "grupos" necesarios en hello token de JWT emitido por Azure AD. Este requisito de notificación debe especificarse en la configuración del paso de servicios de entrega de licencias de varios DRM.
7. Crear una aplicación de ASP.NET MVC que hospedará el reproductor de vídeo. Esta aplicación ASP.NET se protegerán con la autenticación del usuario en el inquilino de Azure Active Directory Hola. Notificaciones adecuadas se incluirán en los tokens de acceso de hello obtenidos después de la autenticación de usuario. Para este paso se recomienda la API de OpenID Connect. Necesita hello tooinstall siguientes paquetes de NuGet:
   * Install-Package Microsoft.Azure.ActiveDirectory.GraphClient
   * Install-Package Microsoft.Owin.Security.OpenIdConnect
   * Install-Package Microsoft.Owin.Security.Cookies
   * Install-Package Microsoft.Owin.Host.SystemWeb
   * Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
8. Crear un reproductor mediante la [API del Reproductor multimedia de Azure](http://amp.azure.net/libs/amp/latest/docs/). [API del Azure Reproductor ProtectionInfo](http://amp.azure.net/libs/amp/latest/docs/) permite toospecify qué toouse de tecnología DRM en otra plataforma DRM.
9. Matriz de pruebas:

| **DRM** | **Browser** | **Resultado de usuario autorizado** | **Resultado de usuario no autorizado** |
| --- | --- | --- | --- |
| **PlayReady** |MS Edge o IE11 en Windows 10 |Correcto |Fail (no superado) |
| **Widevine** |Chrome en Windows 10 |Correcto |Fail (no superado) |
| **FairPlay** |TBD | | |

George Trifonov, del equipo de Servicios multimedia de Azure, ha escrito un blog donde se proporcionan los pasos detallados para configurar Azure Active Directory para una aplicación de reproductor ASP.NET MVC: [Integrate Azure Media Services OWIN MVC based app with Azure Active Directory and restrict content key delivery based on JWT claims](http://gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/)(Integración de una aplicación basada en OWIN MVC de Servicios multimedia de Azure con Azure Active Directory y restricción de la entrega de claves de contenido en función de las notificaciones JWT).

George también ha escrito un blog sobre la [autenticación de tokens de JWT en Servicios multimedia de Azure y Cifrado dinámico](http://gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/). Y este es su [ejemplo sobre la integración de Azure AD con la entrega de claves de Servicios multimedia de Azure](https://github.com/AzureMediaServicesSamples/Key-delivery-with-AAD-integration/).

Para más información sobre Azure Active Directory

* Puede encontrar información para desarrolladores en la [Guía para desarrolladores de Azure Active Directory](../active-directory/active-directory-developers-guide.md).
* Puede encontrar información para administradores en [Administración del directorio de Azure AD](../active-directory/active-directory-administer.md).

### <a name="some-gotchas-in-implementation"></a>Algunos problemas de implementación
Hay algunos problemas "comunes" en la implementación de Hola. Espero Hola después de la lista de "sugerencia" puede ayudarle en caso de encontrarse con problemas de la solución de problemas.

1. La dirección URL del **emisor** debe terminar con **"/"**.  

    **Audiencia** debe ser Hola Id. de cliente de aplicación de Reproductor y también debe agregar **"/"** final Hola de dirección URL del emisor Hola.

        <add key="ida:audience" value="[Application Client ID GUID]" />
        <add key="ida:issuer" value="https://sts.windows.net/[AAD Tenant ID]/" />

    En [JWT descodificador](http://jwt.calebb.net/), debería ver **aud** y **iss** las indicadas a continuación en el token JWT de hello:

    ![Problema 1](./media/media-services-cenc-with-multidrm-access-control/media-services-1st-gotcha.png)
2. Agregar permisos de aplicaciones de toohello en AAD (en la ficha configurar de la aplicación hello). Este paso es necesario para cada aplicación (las versiones local e implementada).

    ![Problema 2](./media/media-services-cenc-with-multidrm-access-control/media-services-perms-to-other-apps.png)
3. Usar a emisor correcto de hello en configuración de la protección de CENC dinámica:

        <add key="ida:issuer" value="https://sts.windows.net/[AAD Tenant ID]/"/>

    Hola método siguiente no funcionará:

        <add key="ida:issuer" value="https://willzhanad.onmicrosoft.com/" />

    Hola GUID es el identificador del inquilino AAD de Hola. Hola GUID se puede encontrar en la ventana emergente de puntos de conexión en el portal de Azure.
4. Otorgue privilegios de notificaciones de pertenencia a grupo. Asegúrese de que en el archivo de manifiesto de aplicación de AAD, tenemos siguiente Hola

    "groupMembershipClaims": "All", (el valor predeterminado de hello es null)
5. Establezca el valor adecuado de TokenType al crear los requisitos de restricción.

        objTokenRestrictionTemplate.TokenType = TokenType.JWT;

    Dado que agregar compatibilidad de JWT (AAD) además de tooSWT (ACS), valor predeterminado de hello TokenType es TokenType.JWT. Si usas SWT/ACS, debe establecer tooTokenType.SWT.

## <a name="additional-topics-for-implementation"></a>Temas adicionales para la implementación
A continuación trataremos algunos temas adicionales de nuestro diseño e implementación.

### <a name="http-or-https"></a>¿HTTP o HTTPS?
Hola aplicación de Reproductor de ASP.NET MVC que creábamos debe admitir siguiente hello:

1. Autenticación de usuario a través de Azure AD que necesita toobe en HTTPS;
2. Intercambio de token de JWT entre cliente y Azure AD que necesita toobe en HTTPS;
3. Adquisición de licencias DRM cliente hello que es necesario toobe en HTTPS si se proporciona entrega de licencia por servicios multimedia de Azure. Por supuesto, el conjunto de productos de PlayReady no impone HTTPS para la entrega de licencias. Si el servidor de licencias de PlayReady está fuera de Servicios multimedia de Azure, se podría usar HTTP o HTTPS.

Por lo tanto, Hola aplicación de Reproductor ASP.NET usará HTTPS como práctica recomendada. Esto significa Hola que Reproductor multimedia de Azure se incluirá en una página en HTTPS. Sin embargo, para la transmisión por secuencias se prefiere HTTP, por lo tanto, necesitamos tooconsider mixto problema contenido.

1. El explorador no permite contenido mixto. Pero, los complementos como Silverlight y OSMF para Smooth y DASH sí lo hacen. Contenido mixto es un problema de seguridad: Esto es debido a las amenazas de toohello de tooinject de capacidad de Hola JS malintencionados que puede producir Hola toobe de datos de cliente en peligro.  Exploradores bloquea de forma predeterminada y hasta ahora hello toowork de manera única alrededor de ella es en el lado del servidor (origen) hello, tooallow todos los dominios (sin tener en cuenta https o http). Probablemente esto tampoco sea una buena idea.
2. Debemos evitar contenido mixto: tanto si se usa HTTP o HTTPS. Al reproducir contenido mixto, silverlightSS tech requiere que se borre una advertencia de contenido mixto. flashSS tech controla el contenido mixto sin advertencia de contenido mixto.
3. Si su punto de conexión de streaming se creó antes de agosto de 2014, no admitirá HTTPS. En este caso, cree y utilice un nuevo punto de conexión de streaming para HTTPS.

En la implementación de referencia de hello, para contenido protegido con DRM, aplicación y la transmisión por secuencias estarán bajo HTTTPS. Para abrir contenido, el Reproductor de hello no necesita autenticación o licencia, así tienen Hola liberty toouse HTTP o HTTPS.

### <a name="azure-active-directory-signing-key-rollover"></a>Sustitución de claves de firma de Azure Active Directory
Se trata de un tootake punto importante en la cuenta de su implementación. Si no se considera en su implementación, sistema de hello completado finalmente dejará de funcionar completamente dentro de al menos 6 semanas.

Azure AD usa sector estándar tooestablish confianza entre sí y las aplicaciones con Azure AD. En concreto, Azure AD utiliza una clave de firma que consta de un par de claves pública y privada. Cuando Azure AD crea un token de seguridad que contiene información acerca del usuario de hello, este token está firmado por Azure AD utilizando su clave privada antes de enviarlo aplicación toohello atrás. tooverify que Hola token es válido y realmente se ha originado en Azure AD, aplicación hello debe validar la firma del token de hello usando la clave pública de hello expuesta por Azure AD que se encuentra en el documento de metadatos de federación del inquilino de Hola. Esta clave pública: y Hola del que se deriva de clave de firma – sean hello uno mismo usan todos los inquilinos en Azure AD.

Información detallada sobre de sustitución de claves de Azure AD puede encontrarse en el documento de hello: [información importante acerca de la sustitución de clave de firma en Azure AD](../active-directory/active-directory-signing-key-rollover.md).

Entre hello [par de claves pública y privada](https://login.microsoftonline.com/common/discovery/keys/),

* se utiliza la clave privada de Hola por Azure Active Directory toogenerate un token JWT;
* clave pública de Hello es utilizado por una aplicación, como servicios de entrega de licencias de DRM en token de JWT de AMS tooverify Hola;

Por motivos de seguridad, Azure Active Directory realiza la rotación de este certificado periódicamente (cada 6 semanas). En el caso de infracciones de seguridad, la sustitución de clave Hola se produce cada vez. Por lo tanto, servicios de entrega de licencia de hello en AMS necesitan clave pública que hello tooupdate usa Azure AD gira el par de claves de hello, en caso contrario, se producirá un error de autenticación de token en AMS y no se emitirá ninguna licencia.

Para ello, es necesario establecer TokenRestrictionTemplate.OpenIdConnectDiscoveryDocument al configurar los servicios de entrega de licencias de DRM.

Hola flujo de tokens de JWT es como a continuación:

1. Azure AD pueda emitir el token de JWT de hello con clave privada actual de Hola para un usuario autenticado;
2. Cuando un reproductor ve una CENC con contenido protegido con DRM-múltiple, buscará en primer lugar token JWT de hello emitido por Azure AD.
3. Reproductor de Hello envía la solicitud de adquisición de licencias con servicios de entrega de toolicense token de JWT de hello en AMS;
4. Servicios de entrega de licencia de Hello en AMS usará una clave pública actual/válida Hola de token JWT de Azure AD tooverify hello, antes de emitir licencias.

Servicios de entrega de licencias DRM se siempre que esté buscando una clave pública actual/válida Hola de Azure AD. clave pública de Hello presentada por Azure AD estará calve de Hola para comprobar un token JWT emitido por Azure AD.

¿Qué ocurre si sustitución de claves de hello ocurre después de AAD genera un token de JWT pero antes de hello JWT token se envía por reproductores tooDRM entrega servicios de licencias en AMS para la comprobación?

Dado que una clave se puede sustituir en cualquier momento, siempre hay más de una clave pública válida disponible en el documento de metadatos de federación de Hola. Entrega de licencias de servicios multimedia de Azure puede usar cualquiera de hello claves especificada en el documento de hello, ya que se puede sustituir una clave pronto, otra puede ser su sustituta y así sucesivamente.

### <a name="where-is-hello-access-token"></a>¿Donde es Hola Token de acceso?
Si observa cómo una aplicación web llama a una aplicación de API en [identidad de aplicación con concesión de credenciales de cliente de OAuth 2.0](../active-directory/develop/active-directory-authentication-scenarios.md#web-application-to-web-api), flujo de autenticación de hello es como a continuación:

1. Un usuario ha iniciado sesión tooAzure AD en la aplicación web de hello (vea hello [tooWeb aplicación de explorador Web](../active-directory/develop/active-directory-authentication-scenarios.md#web-browser-to-web-application).
2. extremo de autorización de Hello Azure AD redirige aplicación Hola usuario agente toohello atrás cliente con un código de autorización. agente de usuario de Hello devuelve el URI de redireccionamiento de la aplicación del cliente de toohello código de autorización.
3. aplicación web de Hello debe tooacquire un token de acceso para que pueda autenticar toohello web API y recuperar recursos de hello deseado. Realiza una tooAzure de solicitud de AD extremo de token y proporcionar credenciales de hello, Id. de cliente y URI de Id. de la aplicación de API de web. Presenta tooprove de código de autorización de Hola que Hola usuario ha dado su consentimiento.
4. Azure AD autentica la aplicación hello y devuelve un token de acceso JWT que es usado toocall hello web API.
5. A través de HTTPS, aplicación web de hello usa Hola devuelve Hola de tooadd de token de acceso JWT cadena JWT con una designación "Bearer" en encabezado de autorización de Hola de toohello web API de hello solicitud. API de web Hello, a continuación, valida el token JWT de Hola y si la validación es correcta, devuelve Hola deseado recursos.

En este flujo de "application identity" API de hello web confía en ese usuario de hello web aplicación Hola autenticado. Por ello, este patrón se conoce como subsistema de confianza. Hola [diagrama en esta página](https://docs.microsoft.com/azure/active-directory/active-directory-protocols-oauth-code) describe cómo el código de autorización concede funciona de flujo.

En la adquisición de licencias con la restricción de token, nos estamos siguiendo Hola mismo patrón de subsistema de confianza. Y servicio de entrega de licencia de hello en los servicios de multimedia de Azure es el recurso de API web de hello, Hola "recurso de back-end" una aplicación web necesita tooaccess. ¿Entonces, donde es el token de acceso de hello?

De hecho, vamos a obtener el token de acceso desde Azure AD. Después de autenticar al usuario correctamente, se devuelve el código de autorización. código de autorización de Hello, a continuación, se usa, junto con la clave de identificador y una aplicación de cliente, tooexchange de token de acceso. Y es el token de acceso de hello para tener acceso a una aplicación de "puntero" que señala o que representa el servicio de entrega de licencias de servicios multimedia de Azure.

Se necesita tooregister y configura aplicación de "puntero" hello en Azure AD Hola pasos siguientes:

1. En el inquilino de hello Azure AD

   * agregue una aplicación (recurso) con la dirección URL de inicio de sesión

   https://[resource_name].azurewebsites.net/ and

   * la URL de identificador de aplicación

   https://[aad_tenant_name].onmicrosoft.com/[resource_name];
2. Agregue una nueva clave para la aplicación de recursos de hello;
3. Actualizar el archivo de manifiesto de aplicación Hola para que la propiedad de groupMembershipClaims hello tiene Hola siguiente valor: "groupMembershipClaims": "All",  
4. En la aplicación de Azure AD de Hola que señala toohello Reproductor web app y en la sección de Hola "permisos tooother aplicaciones", Agregar aplicación de recursos de hello que se agregó en el paso 1 anterior. En "Permisos delegados", active la casilla "Acceso [nombre_de_recurso]". Esto proporciona permiso de aplicación web de hello toocreate los tokens de acceso para tener acceso a la aplicación de recursos de hello. Debe hacerlo para local e implementada la versión de la aplicación web de hello, si está desarrollando a la aplicación web de Visual Studio y Azure.

Por lo tanto, el token JWT de hello emitido por Azure AD es realmente token de acceso de hello para tener acceso a este recurso de "puntero".

### <a name="what-about-live-streaming"></a>¿Y qué pasa con el streaming en vivo?
Hola anterior, nuestro análisis han se centre primero en activos de petición. ¿Y qué pasa con el streaming en vivo?

Hello buenas noticias son que se puede utilizar exactamente Hola mismo diseño e implementación para la protección de streaming en vivo en los servicios de multimedia de Azure, trátelo asset Hola asociado con un programa como un "recurso VOD".

En concreto, es muy conocido que toodo live streaming de servicios multimedia de Azure, debes toocreate un canal y, a continuación, un programa en el canal de Hola. programa hello de toocreate, deberá toocreate un activo que contendrá los archivos activos de hello programa Hola. En orden tooprovide CENC con protección multi-DRM de contenido en directo de hello, todo lo que necesita toodo, se tooapply Hola mismo activo de toohello el programa de instalación/procesamiento como si fuera un "recurso VOD" antes de iniciar el programa de Hola.

### <a name="what-about-license-servers-outside-of-azure-media-services"></a>¿Y qué sucede con los servidores de licencias que están fuera de Servicios multimedia de Azure?
Con frecuencia, puede ocurrir que los clientes inviertan en granjas de servidores de licencias en su propio centro de datos u hospedados por proveedores de servicios DRM. Afortunadamente, protección de contenido de Azure Media Services le permite toooperate en modo híbrido: contenido hospedado y protegido dinámicamente en los servicios de multimedia de Azure, mientras que las licencias DRM se entregan por servidores ajenos a servicios multimedia de Azure. En este caso, hay Hola siguiendo las consideraciones de los cambios:

1. Hola el servicio de Token seguro necesidades tooissue tokens que son aceptables y se pueden comprobar por granja de servidores de licencias de Hola. Por ejemplo, servidores de licencias de Widevine Hola proporcionados por Axinom requiere un token JWT específico que contiene "mensaje de derechos". Por lo tanto, deberá toohave un tooissue STS tal token JWT. los autores de Hello han completado este tipo de implementación y puede encontrar detalles Hola Hola después de documento en [centro de documentación](https://azure.microsoft.com/documentation/): [Axinom utilizando toodeliver Widevine licencias de servicios de multimedia de tooAzure](media-services-axinom-integration.md).
2. Ya no necesita el servicio de entrega de licencia de tooconfigure (ContentKeyAuthorizationPolicy) en servicios multimedia de Azure. Lo que necesita toodo es tooprovide direcciones de URL de adquisición de licencias de hello (para PlayReady, Widevine y FairPlay) al configurar AssetDeliveryPolicy de configuración de CENC con DRM de múltiples.

### <a name="what-if-i-want-toouse-a-custom-sts"></a>¿Qué ocurre si deseo toouse un STS personalizado?
Puede haber varias razones por las que un cliente puede elegir toouse un STS personalizado (servicio de tokens seguro) para proporcionar tokens JWT. Algunas de ellas son:

1. Proveedor de identidad (IDP) usados por el cliente de Hola Hola no admite a STS. En este caso, un STS personalizado puede ser una opción.
2. cliente de Hello tendrá un control más flexible o más estricto en la integración de STS con sistema de facturación de los suscriptores del cliente. Por ejemplo, un operador MVPD puede ofrecer varios paquetes de suscriptor OTT como premium, basic, deportes, operador de hello etc. aconsejable toomatch Hola notificaciones en un token con el paquete de un suscriptor para que sólo el contenido en el paquete adecuado de Hola se pone a disposición. En este caso, un STS personalizado proporciona Hola necesario flexibilidad y control.

Dos cambios necesitan toobe realizado al usar a un STS personalizado:

1. Al configurar el servicio de entrega de licencia para un activo, se necesita la clave de seguridad de Hola de toospecify Hola personalizado STS (más detalles a continuación) en lugar de la clave actual de Hola de Azure Active Directory utiliza para la comprobación.
2. Cuando se genera un token JTW, se especifica una clave de seguridad en lugar de la clave privada de hello del certificado de hello X509 actual en Azure Active Directory.

Hay dos tipos de claves de seguridad:

1. Clave simétrica: Hola misma clave se usa para generar y comprobar un token JWT;
2. Clave asimétrica: un par de claves pública y privada en un certificado se utiliza con la clave privada para cifrar y generar un JWT hello y el token de clave pública para comprobar el token de Hola de X509.

#### <a name="tech-note"></a>Nota técnica
Si usa .NET Framework / C# como plataforma de desarrollo, Hola X509 certificado usado para la clave de seguridad asimétrico debe tener una longitud de clave de al menos 2048. Se trata de un requisito de la clase hello System.IdentityModel.Tokens.X509AsymmetricSecurityKey en .NET Framework. De lo contrario, se producirá Hola tras excepción:

IDX10630: hello 'System.IdentityModel.Tokens.X509AsymmetricSecurityKey' para la firma no puede ser menor que '2048' bits.

## <a name="hello-completed-system-and-test"></a>prueba y del sistema de hello completado
Se le guiará a través de una serie de escenarios en sistema de hello completado-to-end para que los lectores pueden tener una "imagen" del comportamiento de hello basic antes de obtener una cuenta de inicio de sesión.

Hello aplicación web de reproducción y su inicio de sesión pueden encontrarse [aquí](https://openidconnectweb.azurewebsites.net/).

Si lo que necesita es "no integrado" escenario: recursos de vídeo hospedan en servicios multimedia de Azure que son cualquiera desprotegido o protegido con DRM pero sin autenticación de token (emitir un toowhoever de licencia que lo solicite), puede probarlo sin inicio de sesión (cambiando tooHTTP si el vídeo de transmisión por secuencias es a través de HTTP).

Si lo que necesita es el escenario integrado-to-end: recursos de vídeo está bajo protección dinámica de DRM en servicios de multimedia de Azure, con autenticación de token y el token JWT que se genera mediante Azure AD, deberá toologin.

### <a name="user-login"></a>Inicio de sesión de usuario
En orden tootest Hola-to-end DRM sistema integrado, debe toohave una "cuenta" creen o agreguen.

¿Qué cuenta?

Aunque Azure inicialmente permitía el acceso únicamente a usuarios de cuentas Microsoft, ahora permite el acceso a usuarios de ambos sistemas. Esto se hacía manteniendo la confianza de Azure propiedades de todos los hello Azure AD para la autenticación, haciendo que Azure AD autenticar usuarios de la organización y mediante la creación de una relación de federación que Azure AD confía en sistema de identidad de cliente de cuentas de Microsoft de Hola usuarios de consumidor de tooauthenticate. Como resultado, Azure AD es capaz de tooauthenticate cuentas de Microsoft de "Invitado", así como cuentas "nativas" Azure AD.

Puesto que Azure AD confía en el dominio de cuenta de Microsoft (MSA), puede agregar las cuentas de cualquiera de hello después toohello dominios personalizado AD Azure inquilino y usar Hola cuenta toologin:

| **Nombre de dominio** | **Dominio** |
| --- | --- |
| **Dominio de inquilino de Azure AD personalizado** |somename.onmicrosoft.com |
| **Dominio corporativo** |microsoft.com |
| **Dominio de la cuenta Microsoft (MSA)** |outlook.com, live.com, hotmail.com |

Puede ponerse en contacto con cualquiera de los autores de hello toohave una cuenta que se crea o se agrega.

A continuación se muestran capturas de pantalla de Hola de páginas de inicio de sesión diferente utilizadas diferentes cuentas de dominio.

**Cuenta de dominio de inquilino de AD de Azure personalizada**: en este caso, verá la página de inicio de sesión personalizado Hola de dominio del inquilino Hola personalizado AD de Azure.

![Cuenta de dominio de inquilino de Azure AD personalizado](./media/media-services-cenc-with-multidrm-access-control/media-services-ad-tenant-domain1.png)

**Cuenta de dominio de Microsoft con tarjeta inteligente**: en este caso verá la página de inicio de sesión de hello personalizar Microsoft corporativa TI con la autenticación en dos fases.

![Cuenta de dominio de inquilino de Azure AD personalizado](./media/media-services-cenc-with-multidrm-access-control/media-services-ad-tenant-domain2.png)

**Cuenta de Microsoft (MSA)**: en este caso, verá la página de inicio de sesión de Hola de Account de Microsoft para los consumidores.

![Cuenta de dominio de inquilino de Azure AD personalizado](./media/media-services-cenc-with-multidrm-access-control/media-services-ad-tenant-domain3.png)

### <a name="using-encrypted-media-extensions-for-playready"></a>Uso de extensiones multimedia cifradas para PlayReady
En un explorador moderno extensiones con medios cifrada (EME) para la compatibilidad, por ejemplo, el Explorador de Internet Explorer 11 en Windows 8.1 o superior y Microsoft Edge en Windows 10, PlayReady será de PlayReady hello DRM subyacente para EME.

![Uso de EME para PlayReady](./media/media-services-cenc-with-multidrm-access-control/media-services-eme-for-playready1.png)

área de Reproductor oscuro Hello es debido a que la protección PlayReady impide que uno de realizar la captura de pantalla de vídeo protegido de hechos de toohello.

Hello pantalla siguiente muestra hello Reproductor complementos y soporte técnico MSE/EME.

![Uso de EME para PlayReady](./media/media-services-cenc-with-multidrm-access-control/media-services-eme-for-playready2.png)

EME en Microsoft Edge e Internet Explorer 11 en Windows 10 permiten invocar [PlayReady SL3000](https://www.microsoft.com/playready/features/EnhancedContentProtection.aspx/) en dispositivos de Windows 10 que lo admitan. PlayReady SL3000 desbloquea flujo Hola de contenido premium mejorado (4K, HDR, etc.) y nuevos modelos de entrega de contenido (ventana temprana para contenido mejorado).

Centrarse en los dispositivos de Windows hello: PlayReady es Hola solo DRM en hello HW disponible en dispositivos de Windows (PlayReady SL3000). Un servicio de streaming puede usar PlayReady mediante EME o una aplicación de UWP y ofrecer una mayor calidad de vídeo con PlayReady SL3000 que otro DRM. Por lo general, contenido de 2K fluirá a través de Chrome o Firefox y 4 K contenido a través de Microsoft Edge/IE11 o una aplicación de UWP en Hola mismo dispositivo (según la configuración del servicio y la implementación).

#### <a name="using-eme-for-widevine"></a>Uso de EME para Widevine
En un explorador moderno con compatibilidad EME/Widevine, por ejemplo, Chrome 41 + en Windows 10, Windows 8.1, Mac OSX Yosemite y Chrome en 4.4.4 Android, Google Widevine es hello DRM detrás EME.

![Uso de EME para Widevine](./media/media-services-cenc-with-multidrm-access-control/media-services-eme-for-widevine1.png)

Tenga en cuenta que Widevine no impide la realización de capturas de pantalla de vídeo protegido.

![Uso de EME para Widevine](./media/media-services-cenc-with-multidrm-access-control/media-services-eme-for-widevine2.png)

### <a name="not-entitled-users"></a>Usuarios no autorizados
Si un usuario no es miembro del grupo "Usuarios"titulada ", usuario de hello no será capaz de toopass"comprobación de derechos"y servicio de licencias de DRM de múltiples Hola rechazará la licencia solicitada de hello tooissue tal y como se muestra a continuación. Hola descripción detallada es "adquirir licencias no se pudo", que es como se ha diseñado.

![Usuarios no autorizados](./media/media-services-cenc-with-multidrm-access-control/media-services-unentitledusers.png)

### <a name="running-custom-secure-token-service"></a>Ejecución del servicio de token seguro personalizado
Para el escenario de Hola de ejecución personalizado Token servicio seguro (STS), token de JWT de Hola se emitirá por STS personalizado Hola con clave simétrica o asimétrica.

caso de Hello del uso de clave simétrica (con Chrome):

![Ejecución del STS personalizado](./media/media-services-cenc-with-multidrm-access-control/media-services-running-sts1.png)

Hola caso del uso de clave asimétrica a través de un X509 de certificados (mediante el explorador moderno de Microsoft).

![Ejecución del STS personalizado](./media/media-services-cenc-with-multidrm-access-control/media-services-running-sts2.png)

En ambos Hola por encima de los casos, la autenticación de usuario sigue Hola igual: a través de Azure AD. Hola única diferencia es que se emiten tokens JWT Hola STS personalizado en lugar de Azure AD. Por supuesto, al configurar la protección de CENC dinámico, restricción Hola de servicio de entrega de licencia especifica tipo hello de token JWT, clave simétrica o asimétrica.

## <a name="summary"></a>Resumen
En este documento, hemos examinado el CENC con varios DRM nativos y el control de acceso mediante la autenticación con tokens: su diseño y su implementación mediante Azure, Servicios multimedia de Azure y el Reproductor multimedia de Azure.

* Se presenta un diseño de referencia que contiene todos los componentes necesarios de hello en un subsistema DRM/CENC;
* y una implementación de referencia en Azure, Servicios multimedia de Azure y el Reproductor multimedia de Azure.
* También se describen algunos de los temas directamente relacionadas con la implementación y diseño Hola.

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
 
