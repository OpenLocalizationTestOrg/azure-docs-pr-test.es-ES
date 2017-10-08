---
title: "conectores de Proxy de aplicación de Azure AD aaaUnderstand | Documentos de Microsoft"
description: "Abarca conceptos básicos de hello acerca de los conectores de Proxy de aplicación de Azure AD."
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
ms.openlocfilehash: 294cb26803ef7cf8be9f3af0678d6d2e64f6cc14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-ad-application-proxy-connectors"></a>Descripción de los conectores del Proxy de aplicación de Azure AD

Los conectores son los que hacen posible el Proxy de aplicación de Azure AD. Son toodeploy simple, fácil y mantener y super eficaz. Este artículo describe qué conectores son, cómo funcionan y algunas sugerencias sobre cómo toooptimize la implementación. 

## <a name="what-is-an-application-proxy-connector"></a>Qué es un conector proxy de aplicación

Los conectores son agentes ligeros que están sentados en local y facilitan el servicio de Proxy de aplicación de toohello de conexión de salida de hello. Conectores deben instalarse en un servidor de Windows que tenga la aplicación de access toohello back-end. Puede organizar los conectores en grupos de conectores, con cada grupo de aplicaciones de toospecific de tráfico de control. Equilibrio de carga de conectores automáticamente y puede ayudar a toooptimize la estructura de red. 

## <a name="requirements-and-deployment"></a>Requisitos e implementación

Proxy de aplicación de toodeploy correctamente, necesita al menos un conector, pero se recomienda dos o más para obtener una mayor resistencia. Instale el conector de hello en un Windows Server 2012 R2 o una máquina de 2016. Conector de Hello necesita toobe puede toocommunicate con el servicio de Proxy de aplicación Hola, así como aplicaciones locales de Hola que se publican. 

Para obtener más información acerca de los requisitos de red de hello para el servidor de conector de hello, consulte [comenzar con el Proxy de aplicación e instalar un conector](active-directory-application-proxy-enable.md).

## <a name="maintenance"></a>Mantenimiento
Hello conectores y servicio de Hola se encargan de todas las tareas de alta disponibilidad de Hola. Se pueden agregar o quitar de forma dinámica. Cada vez que llega una solicitud nueva es tooone enrutado de conectores de Hola que esté disponible. Si un conector no está disponible temporalmente, no responde toothis tráfico.

conectores de Hello no tienen estados y no tengan ningún dato de configuración en el equipo de Hola. Hello solo los datos que almacena están Hola configuración para conectar el servicio de Hola y su certificado de autenticación. Cuando conecta el servicio de toohello, se extraen todos los datos de configuración de hello necesario y actualización cada dos minutos.

Conectores también sondean Hola servidor toofind si hay una versión más reciente del conector de Hola. Si se encuentra uno, los conectores de hello actualizar por sí mismos.

Puede supervisar los conectores de la máquina de Hola se ejecutan en, con el registro de eventos de Hola y contadores de rendimiento. O bien, puede ver su estado de página de Proxy de aplicación Hola de hello portal de Azure:

 ![Conectores del Proxy de aplicación de Azure AD](./media/application-proxy-understand-connectors/app-proxy-connectors.png)

No es necesario toomanually eliminar conectores que no se utilicen. Cuando se está ejecutando un conector, permanece activa tal y como se conecta el servicio toohello. Los conectores que no se están usando se etiquetan como _inactivos_ y se quitan tras 10 días de inactividad. Si desea toouninstall un conector, no obstante, desinstale los servicios del conector de Hola y Hola actualizador de hello servidor. Reinicie el servicio de equipo toofully remove Hola.

## <a name="automatic-updates"></a>Actualizaciones automáticas

Azure AD proporciona las actualizaciones automáticas para todos los conectores de Hola que implemente. Hola actualizador de conector del Proxy de aplicación se está ejecutando, siempre y cuando sus conectores se actualizan automáticamente. Si no ve Hola servicio actualizador del conector en el servidor, deberá demasiado[volver a instalar el conector](active-directory-application-proxy-enable.md) tooget todas las actualizaciones. 

Si no desea toowait para un conector de tooyour toocome de actualización automática, puede realizar una actualización manual. Vaya toohello [página de descarga de conector](https://download.msappproxy.net/subscription/d3c8b69d-6bf7-42be-a529-3fe9c2e70c90/connector/download) en donde el conector es buscar y seleccione el servidor de hello **descargar**. Este proceso inicia una actualización para el conector local Hola. 

Para que los inquilinos con varios conectores, actualizaciones automáticas de Hola tener como destino un conector a la vez en cada grupo tooprevent un tiempo de inactividad en el entorno. 

Puede experimentar un tiempo de inactividad cuando el conector se actualiza si:  
- Solo tiene un conector. tooavoid este tiempo de inactividad y mejorar la alta disponibilidad, se recomienda instalar un segundo conector y [crear un grupo de conectores](active-directory-application-proxy-connectors-azure-portal.md).  
- Un conector estaba en medio de Hola de una transacción cuando se inició la actualización de Hola. Aunque se pierde la transacción inicial de hello, el explorador automáticamente debería intentar realizar la operación de Hola o puede actualizar la página. Cuando se vuelve a enviar la solicitud de hello, el tráfico de hello es conector de copia de seguridad de tooa enrutado.

## <a name="creating-connector-groups"></a>Creación de grupos de conectores

Grupos de conectores le permiten aplicaciones específicas del tooserve tooassign conectores específicos. Puede agrupar un número de conectores y, a continuación, asigne a cada grupo de tooa de aplicación. 

Grupos de conectores facilitan más fácil toomanage de implementaciones grandes. También mejoran la latencia para los inquilinos que tienen las aplicaciones hospedadas en distintas regiones, porque se pueden crear grupos de conectores basadas en ubicación tooserve local sólo aplicaciones. 

toolearn más información acerca de los grupos de conectores, consulte [publicar aplicaciones en ubicaciones mediante grupos de conectores y redes independientes](active-directory-application-proxy-connectors-azure-portal.md).

## <a name="security-and-networking"></a>Seguridad y redes

Conectores pueden instalarse en cualquier ubicación de red de Hola que les permita el servicio de Proxy de aplicación de toosend solicitudes toohello. Lo importante es que el equipo Hola ejecuta el conector de hello también tiene acceso tooyour aplicaciones. Puede instalar conectores dentro de la red corporativa o en una máquina virtual que se ejecuta en la nube de Hola. Los conectores se pueden ejecutar en una red perimetral (DMZ), pero no es necesario, ya que todo el tráfico es saliente, así que la red se mantiene protegida.

Los conectores solo envían solicitudes salientes. se envía el tráfico saliente Hello toohello servicio de Proxy de aplicación y toohello aplicaciones publicadas. No es necesario tooopen puertos de entrada porque el tráfico fluye ambas formas, una vez establecida una sesión. No tiene tooset de equilibrio de carga entre los conectores de Hola o configurar el acceso entrante a través de los servidores de seguridad. 

Para más información sobre cómo configurar reglas de firewall de salida, vea [Trabajo con servidores proxy locales existentes](application-proxy-working-with-proxy-servers.md).

Hola de uso [herramienta de prueba de Azure AD aplicación Proxy conector puertos](https://aadap-portcheck.connectorporttest.msappproxy.net/) tooverify que el conector puede comunicarse con servicio de Proxy de aplicación Hola. Como mínimo, asegúrese de que región de EE. UU. Central de Hola y Hola región más cercana tooyou tienen todas las marcas de verificación verde. Además, cuantas más marcas de verificación verde haya, mayor resistencia habrá. 

## <a name="performance-and-scalability"></a>Rendimiento y escalabilidad

Escala de hello servicio Proxy de aplicación es transparente, pero la escala es un factor para conectores. Debe toohave suficiente tráfico pico de toohandle de conectores. Sin embargo, no es necesario tooconfigure equilibrio de carga porque equilibrar la carga automáticamente todos los conectores dentro de un grupo de conectores.

Puesto que los conectores son sin estado, no se ven afectados por número de Hola de los usuarios o las sesiones. En su lugar, responden toohello número de solicitudes y su tamaño de carga. En el caso del tráfico web estándar, una máquina puede controlar en promedio unas dos mil solicitudes por segundo. capacidad específica de Hello depende de las características de equipo exacto de Hola. 

rendimiento del conector Hola viene determinada por la red y de CPU. Rendimiento de la CPU es necesario para el cifrado SSL y el descifrado, mientras que las redes son aplicaciones de toohello de conectividad rápida tooget importante y el servicio en línea de hello en Azure.

En cambio, la memoria no supone un problema para los conectores. servicio en línea Hello se encarga de gran parte del procesamiento de Hola y todo el tráfico no autenticado. Todo lo que puede realizarse en la nube de Hola se realiza en la nube de Hola. 

Otro factor que afecta al rendimiento es la calidad de Hola de las redes de hello entre conectores hello, incluidos: 

* **Hola servicio en línea**: conexiones lentas o de latencia alta toohello servicio de Proxy de aplicación en el rendimiento del conector de Azure influencia Hola. Para obtener el mejor rendimiento de hello, conectar tooAzure de su organización con Express Route. En caso contrario, tiene el equipo de red Asegúrese de que tooAzure las conexiones se tratan como más eficaz posible. 
* **Hola aplicaciones back-end**: en algunos casos, hay servidores proxy adicionales entre el conector de Hola y las aplicaciones de back-end de Hola que pueden ralentizar o impedir las conexiones. tootroubleshoot este escenario, abra un explorador desde el servidor de conector de Hola y probar tooaccess Hola aplicación. Si se ejecutan conectores de hello en Azure pero las aplicaciones de hello son locales, experiencia de hello podría no ser lo que espera que los usuarios.
* **controladores de dominio de Hola**: si los conectores de hello efectuar el SSO con la delegación limitada de Kerberos, ponerse en contacto con los controladores de dominio de hello antes de enviar Hola solicitud toohello back-end. conectores de Hello tienen una memoria caché de vales de Kerberos, pero en un entorno de ocupado la capacidad de respuesta de Hola Hola de controladores de dominio puede afectar al rendimiento. Este problema es más común en el caso de los conectores que se ejecutan en Azure pero se comunican con controladores de dominio que están en local. 

Para más información sobre la optimización de la red, vea [Consideraciones sobre la topología de red al utilizar el Proxy de aplicación de Azure Active Directory](application-proxy-network-topology-considerations.md).

## <a name="domain-joining"></a>Unión a dominio

Los conectores se pueden ejecutar en un equipo que no esté unido a dominio. Sin embargo, si desea que solo inicio de sesión (SSO) tooapplications que usan la autenticación de Windows integrada (IWA), necesita un equipo unido al dominio. En este caso, las máquinas de conector de hello deben ser tooa Unidos a un dominio que puede llevar a cabo [Kerberos](https://web.mit.edu/kerberos) la delegación restringida en nombre de los usuarios de Hola para hello aplicaciones publicadas.

Conectores también pueden ser toodomains combinadas o bosques que tienen una relación de confianza parcial o controladores de dominio de sólo tooread.

## <a name="connector-deployments-on-hardened-environments"></a>Implementaciones del conector en entornos protegidos

Por lo general, la implementación del conector es sencilla y no requiere ninguna configuración especial. Sin embargo, hay algunas condiciones únicas que deben tenerse en cuenta:

* Las organizaciones que limitan el tráfico saliente Hola deben [abrir los puertos necesarios](active-directory-application-proxy-enable.md#open-your-ports).
* Máquinas conformes a FIPS podrían ser necesario toochange su tooallow configuración Hola toogenerate de procesos de conector y almacenar un certificado.
* Las organizaciones que bloquear su entorno basada en procesos de Hola que Hola problema las solicitudes de red tienen toomake Asegúrese de que ambos servicios del conector son puertos habilitado tooaccess todas las necesarias y las direcciones IP.
* En algunos casos, proxy de reenvío de salida puede interrumpir la autenticación de certificado bidireccional de Hola y provocar Hola comunicación toofail.

## <a name="connector-authentication"></a>Autenticación de conector

tooprovide un servicio seguro, los conectores tienen tooauthenticate hacia el servicio de Hola y servicio hello tiene tooauthenticate hacia el conector de Hola. Esta autenticación se realiza mediante certificados de cliente y servidor cuando conectores Hola inician la conexión de Hola. Nombre de usuario y la contraseña de este administrador de Hola de manera no se almacenan en la máquina de conector de Hola.

los certificados de Hello usados son servicio de Proxy de aplicación de toohello específico. Que se crean durante el registro inicial de Hola y son automáticamente renovado por los conectores de hello cada dos meses. 

Si no está conectado un conector de servicio toohello durante varios meses, sus certificados puede estar obsoleta. En este caso, desinstale y vuelva a instalar el registro de tootrigger del conector de Hola. Puede ejecutar Hola siga los comandos de PowerShell:

```
Import-module AppProxyPSModule
Register-AppProxyConnector
```

## <a name="under-hello-hood"></a>Bajo el paraguas de Hola

Conectores se basan en el Proxy de aplicación Web de Windows Server, por lo que tienen la mayoría de Hola mismo herramientas de administración, incluidos los registros de eventos de Windows

 ![Administrar registros de eventos con hello Visor de eventos](./media/application-proxy-understand-connectors/event-view-window.png)

y contadores de rendimiento de Windows. 

 ![Agregue contadores toohello conector con hello Monitor de rendimiento](./media/application-proxy-understand-connectors/performance-monitor.png)

conectores de Hello tienen administradores y sesión de registros. registros de administración de Hello son los errores y eventos clave. los registros de sesión de Hello incluyen todas las transacciones de Hola y sus detalles de procesamiento. 

registros de hello toosee, vaya toohello Visor de eventos, abra hello **vista** menú y habilitar **mostrar analíticos y de depuración registros**. A continuación, habilitarlas toostart la recopilación de eventos. Estos registros no aparecen en el Proxy de aplicación Web en Windows Server 2012 R2, como conectores Hola se basan en una versión más reciente.

Puede examinar el estado de saludo del servicio de hello en la ventana de servicios de Hola. Conector de Hello consta de dos servicios de Windows: conector real de Hola y actualizador de Hola. Dos de ellos deben ejecutar todo el tiempo Hola.

 ![Local de servicios de Azure AD](./media/application-proxy-understand-connectors/aad-connector-services.png)

## <a name="next-steps"></a>Pasos siguientes


* [Publicación de aplicaciones en redes independientes y ubicaciones mediante grupos de conectores](active-directory-application-proxy-connectors-azure-portal.md)
* [Trabajo con servidores proxy locales existentes](application-proxy-working-with-proxy-servers.md)
* [Solución de problemas y mensajes de error de Proxy de aplicación](active-directory-application-proxy-troubleshoot.md)
* [¿Cómo toosilently instalar Hola conector del Proxy de aplicación de Azure AD](active-directory-application-proxy-silent-installation.md)

