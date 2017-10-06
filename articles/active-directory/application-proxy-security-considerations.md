---
title: "Consideraciones de aaaSecurity para el Proxy de aplicación de Azure AD | Documentos de Microsoft"
description: "Se tratan las consideraciones de seguridad al utilizar el Proxy de aplicación de Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: ebd14b9d1fc8f4629c5916e5a910595727d935d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="security-considerations-for-accessing-apps-remotely-with-azure-ad-application-proxy"></a>Consideraciones de seguridad al obtener acceso a aplicaciones de forma remota con el Proxy de aplicación de Azure AD

En este artículo se explica el modo en que el proxy de aplicación de Azure Active Directory proporciona un servicio seguro para la publicación y el acceso a las aplicaciones de forma remota.

Hola siguiente diagrama muestra cómo Azure AD permite a las aplicaciones locales de tooyour de acceso remoto seguro.

 ![Diagrama de acceso remoto seguro a través del Proxy de aplicación de Azure AD](./media/application-proxy-security-considerations/secure-remote-access.png)

## <a name="security-benefits"></a>Ventajas de seguridad

El Proxy de aplicación de Azure AD ofrece Hola siguiendo las ventajas de seguridad:

### <a name="authenticated-access"></a>Acceso autenticado 

Si elige toouse Azure Active Directory autenticación previa, solo las conexiones autenticadas pueden acceder a la red.

El Proxy de aplicación de Azure AD se basa en hello Azure AD token servicio seguridad (STS) para toda la autenticación.  Autenticación previa, por su propia naturaleza, bloquea un número significativo de ataques anónimos, porque solo identidades autenticadas pueden tener acceso a la aplicación de back-end de hello.

Si elige el acceso directo como método de autenticación previa, no disfruta de esta ventaja. 

### <a name="conditional-access"></a>Acceso condicional

Aplicar controles de directiva más completos antes de que las conexiones se establecen tooyour red.

Con [acceso condicional](active-directory-conditional-access-azuread-connected-apps.md), puede definir restricciones en el tráfico que permitían tooaccess las aplicaciones de back-end. Puede crear directivas que restrinjan los inicios de sesión en función de la ubicación, el nivel de autenticación y el perfil de riesgo del usuario.

También puede utilizar directivas de acceso condicional tooconfigure la autenticación multifactor, agregar otra capa de autenticaciones de usuario de seguridad tooyour. 

### <a name="traffic-termination"></a>Terminación del tráfico

Todo el tráfico se termina en la nube de Hola.

Dado que el Proxy de aplicación de Azure AD es un servidor proxy inverso, todas las aplicaciones de servidor tooback de tráfico se termina en el servicio de Hola. Hello puede obtener restablece sesión solo con el servidor de back-end de hello, lo que significa que los servidores back-end no están expuestos tráfico toodirect HTTP. Esta configuración implica que está mejor protegido frente a ataques dirigidos.

### <a name="all-access-is-outbound"></a>Todo el acceso es de salida. 

Red corporativa de tooopen las conexiones entrantes toohello no es necesario.

Conectores de Proxy de aplicación sólo utilizan servicio de Proxy de aplicación de Azure AD toohello las conexiones salientes, lo que significa que no hay tooopen puertos del firewall para las conexiones entrantes. Servidores proxy tradicional requiere una red perimetral (también conocido como *DMZ*, *zona desmilitarizada*, o *subred filtrada*) y permite el acceso toounauthenticated conexiones en el perímetro de la red de Hola. Este escenario se requiere muchos inversión adicional en la aplicación web tráfico tooanalyze de productos de firewall y ofrece suma protecciones toohello entorno. Con Proxy de aplicación no se necesita una red perimetral, ya que todas las conexiones son de salida y tienen lugar a través de un canal seguro.

Para más información sobre los conectores, consulte [Descripción de los conectores del Proxy de aplicación de Azure AD](application-proxy-understand-connectors.md).

### <a name="cloud-scale-analytics-and-machine-learning"></a>Análisis de escala en la nube y aprendizaje automático 

Obtenga una protección de seguridad avanzada.

Dado que forma parte de Azure Active Directory, puede aprovechar el Proxy de aplicación [Azure AD Identity Protection](active-directory-identityprotection.md), con intelligence controladas por el aprendizaje de máquina y los datos de Microsoft Security Response Center hello y unidad de crímenes digitales. Juntos identificamos de manera proactiva las cuentas en peligro y ofrecemos protección en tiempo real frente a inicios de sesión de alto riesgo. Tomamos en consideración diversos factores, como el acceso desde dispositivos infectados y a través de redes anónimas, y desde ubicaciones atípicas y poco probables.

Muchos de estos informes y eventos ya están disponibles a través de una API para la integración con los sistemas de información de seguridad y administración de eventos (SIEM).

### <a name="remote-access-as-a-service"></a>Acceso remoto en forma de servicio

No es necesario tooworry sobre cómo mantener y servidores locales de la aplicación de revisiones.

El software al que no se aplican revisiones sigue siendo objeto de un gran número de ataques. El Proxy de aplicación de Azure AD es un servicio de escala de Internet que es propietario de Microsoft, por lo que siempre obtendrá las actualizaciones y revisiones de seguridad más recientes de Hola.

seguridad de hello tooimprove de aplicaciones publicadas por el Proxy de aplicación de Azure AD, se bloquea robots de rastreador (crawler) web de indización y el archivado de sus aplicaciones. Cada vez que un robot de agente de búsqueda intenta recuperar la configuración del robot de una aplicación publicada, el Proxy de aplicación responde con un archivo robots.txt que incluye `User-agent: * Disallow: /`.

## <a name="under-hello-hood"></a>Bajo el paraguas de Hola

El Proxy de aplicación de Azure AD consta de dos partes:

* Hola servicio en la nube: este servicio se ejecuta en Azure y es donde se realizan las conexiones de cliente o usuario externo Hola.
* [Hola conector local](application-proxy-understand-connectors.md): un componente local, el conector de hello escucha las solicitudes de servicio de Proxy de aplicación hello Azure AD y administra aplicaciones internas de las conexiones toohello. 

Se establece un flujo entre el conector de Hola y el servicio de Proxy de aplicación Hola cuando:

* en primer lugar se configura el conector de Hola.
* Conector de Hello extrae información de configuración de servicio de Proxy de aplicación Hola.
* Un usuario tiene acceso a una aplicación publicada.

>[!NOTE]
>Todas las comunicaciones se producen a través de SSL, y siempre se originan en hello conector toohello servicio Proxy de aplicación. servicio de Hello sólo es de salida.

Conector de Hello usa un toohello tooauthenticate de certificado de cliente servicio de Proxy de aplicación para casi todas las llamadas. Hello solo excepción toothis proceso es paso de la instalación inicial de hello, donde se establece el certificado de cliente de Hola.

### <a name="installing-hello-connector"></a>Instalar el conector de Hola

Cuando primero se instala el conector de hello, Hola después de eventos de flujo tienen lugar:

1. servicio de toohello de registro de Hello conector ocurre como parte de hello instalación del conector de Hola. Los usuarios es tooenter solicitada sus credenciales de administrador de Azure AD. El token obtenido desde esta autenticación, a continuación, se presenta el servicio de Proxy de aplicación de Azure AD toohello.
2. Hola servicio Proxy de aplicación se evalúa como token Hola. Garantiza que el usuario Hola sea un administrador de la compañía dentro de inquilino de Hola Hola token haya sido emitido para. Si el usuario de hello no es un administrador, se finaliza el proceso de Hola.
3. Conector de Hello genera una solicitud de certificado de cliente y lo pasa, junto con hello toohello de token, el servicio de Proxy de aplicación. servicio de Hola a su vez comprueba el token de Hola y firma la solicitud de certificado de cliente de Hola.
4. Conector de Hello usa certificados de cliente de hello para la comunicación posterior con hello servicio Proxy de aplicación.
5. Conector de Hello lleva a cabo una extracción de datos de configuración de sistema de saludo inicial del servicio de hello usando su certificado de cliente y estará listo tootake solicitudes.

### <a name="updating-hello-configuration-settings"></a>Actualizar valores de configuración de Hola

Cada vez que Hola servicio Proxy de aplicación actualiza la configuración de hello, Hola después de eventos de flujo tienen lugar:

1. Conector de Hello conecta toohello extremo de configuración dentro de hello servicio Proxy de aplicación mediante su certificado de cliente.
2. Una vez que se validó el certificado de cliente de hello, Hola servicio Proxy de aplicación devuelve toohello conector de datos de configuración (por ejemplo, grupo de conectores de Hola que Hola conector debe formar parte de).
3. Si el certificado actual de hello es más de 180 días de antigüedad, conector Hola genera una nueva solicitud de certificado, que actualiza eficazmente certificado de cliente de hello cada 180 días.

### <a name="accessing-published-applications"></a>Acceso a aplicaciones publicadas

Cuando los usuarios tienen acceso a una aplicación publicada, hello siguientes eventos tienen lugar entre el servicio de Proxy de aplicación Hola y el conector del Proxy de aplicación de hello:

1. [servicio de Hello autentica al usuario Hola aplicación hello](#the-service-checks-the-configuration-settings-for-the-app)
2. [servicio de Hello realiza una solicitud en cola del conector Hola](#The-service-places-a-request-in-the-connector-queue)
3. [Un conector procesa la solicitud de Hola de cola de Hola](#the-connector-receives-the-request-from-the-queue)
4. [Conector de Hello esperará una respuesta](#the-connector-waits-for-a-response)
5. [Hola secuencias datos toohello usuario](#the-service-streams-data-to-the-user)

sigan leyendo toolearn más información acerca de lo que tiene lugar en cada uno de estos pasos.


#### <a name="1-hello-service-authenticates-hello-user-for-hello-app"></a>1. servicio de Hola autentica el usuario de hello para la aplicación hello

Si configuró Hola aplicación toouse acceso directo como su método de autenticación previa, se omiten los pasos de hello en esta sección.

Si configuró Hola aplicación toopreauthenticate con Azure AD, los usuarios son redirigido toohello tooauthenticate de STS de Azure AD y hello pasos siguientes tienen lugar:

1. Proxy de aplicación comprueba los requisitos de la directiva de acceso condicional para aplicaciones específicas de Hola. Este paso garantiza que se ha asignado a ese usuario de hello toohello aplicación. Si se requiere la verificación en dos pasos, secuencia de autenticación de hello pide a usuario Hola un segundo método de autenticación.

2. Una vez que han pasado todas las comprobaciones, Hola STS en Azure AD emite un token firmado para la aplicación hello y redirecciones Hola usuario espera toohello servicio Proxy de aplicación.

3. Proxy de aplicación comprueba que ese token Hola se emitió la aplicación de hello toocorrect. También realiza comprobaciones de otros, como asegurarse de esa Hola token se firmó con Azure AD y que esté aún dentro de ventana válido de Hola.

4. Proxy de aplicación establece una tooindicate de cookie de autenticación cifrada que se ha producido la aplicación de toohello de autenticación. Hello cookie incluye una marca de tiempo de expiración que se basa en el token de Hola de Azure AD y otros datos, tales como nombre de usuario de Hola Hola autenticación se basa en. Hola cookie se cifra con una clave privada que se conoce solo toohello servicio Proxy de aplicación.

5. Aplicación Proxy redirecciones Hola usuario espera toohello la dirección URL solicitada originalmente.

Si se produce un error en cualquier parte de los pasos de autenticación previa de hello, se deniega la solicitud del usuario de Hola y usuario Hola se muestra un mensaje que indica el origen de Hola de problema de Hola.


#### <a name="2-hello-service-places-a-request-in-hello-connector-queue"></a>2. servicio de Hola realiza una solicitud en cola del conector Hola

Conectores de mantener un servicio Proxy de aplicación de toohello Abrir conexión saliente. Cuando llega una solicitud, servicio de hello pone en cola solicitud hello en una de las conexiones abiertas de Hola para hello conector toopick seguridad.

solicitud de Hello incluye elementos de la aplicación hello, como los encabezados de solicitud de hello, datos de la cookie de hello cifrado, Hola usuario realizando la solicitud de Hola y Hola identificador de solicitud Aunque los datos de cookie cifrada Hola se envían con solicitud de hello, propia cookie de autenticación hello no lo es.

#### <a name="3-hello-connector-processes-hello-request-from-hello-queue"></a>3. conector de Hola procesa la solicitud de Hola de cola de Hola. 

En función de la solicitud de hello, Proxy de aplicación realiza una de hello siguientes acciones:

* Si la solicitud de hello es una operación sencilla (por ejemplo, no hay ningún dato dentro del cuerpo de hello con un RESTful *obtener* solicitud), el conector de hello, un recurso interno del destino de conexión toohello y, a continuación, espera una respuesta.

* Si solicitud hello tiene datos asociados a él en el cuerpo de hello (por ejemplo, un RESTful *POST* operación), conector Hola hace una conexión de salida mediante la instancia de Proxy de aplicación de toohello del certificado de cliente de Hola. Hace que estos datos de conexión toorequest hello y abrir un recurso interno de toohello de conexión. Después de recibir la solicitud de Hola de conector de hello, servicio de Proxy de aplicación Hola comienza a aceptar el contenido de usuario de Hola y reenvía el conector de toohello de datos. Conector de Hello, reenvía a su vez, recursos internos de hello datos toohello.

#### <a name="4-hello-connector-waits-for-a-response"></a>4. conector de Hola esperará una respuesta.

Una vez que la solicitud de Hola y transmisión de toohello todo el contenido final es completando, conector Hola esperará una respuesta.

Después de recibir una respuesta, conector Hola hace que un servicio de Proxy de aplicación de conexión de salida toohello, tooreturn Hola detalles del encabezado y empezar a transmitir datos de valor devuelto de saludo.

#### <a name="5-hello-service-streams-data-toohello-user"></a>5. Hola servicio secuencias datos toohello el usuario. 

Algún procesamiento de la aplicación hello puede producirse aquí. Si configuró las direcciones URL o encabezados de tootranslate de Proxy de aplicación en la aplicación, que el procesamiento se produce según sea necesario durante este paso.


## <a name="next-steps"></a>Pasos siguientes

[Consideraciones sobre la topología de red al usar el Proxy de aplicación de Azure Active Directory](application-proxy-network-topology-considerations.md)

[Descripción de los conectores del Proxy de aplicación de Azure AD](application-proxy-understand-connectors.md)
