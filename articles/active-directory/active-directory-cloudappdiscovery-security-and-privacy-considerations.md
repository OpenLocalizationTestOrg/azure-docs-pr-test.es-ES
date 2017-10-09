---
title: "aaaCloud aplicación detección consideraciones de seguridad y privacidad | Documentos de Microsoft"
description: Este tema describe la seguridad de Hola y privacidad consideraciones relacionadas tooCloud App Discovery.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 2fce5c82-d3de-4097-808f-40214768df9e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 33659e85bd2cf4294e443512e69a85401f7c53f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-app-discovery-security-and-privacy-considerations"></a>Consideraciones de seguridad y privacidad de Cloud App Discovery
Microsoft está comprometido tooprotecting su privacidad y los datos, al tiempo que ofrece software y los servicios que le ayuden a administrar la seguridad de Hola de su organización.  
Reconocemos que cuando confía sus datos tooothers, esa confianza requiere inversiones en ingeniería de seguridad rigurosa y tooback conocimientos sobre él.
Microsoft adhiere a las directrices de seguridad y cumplimiento de normas de toostrict de software segura desarrollo del ciclo de vida prácticas toooperating un servicio.  
 La seguridad y la protección de los datos son prioritarias en Microsoft.

En este tema se explica cómo se recopilan, procesan y protegen los datos dentro de Cloud App Discovery de Azure Active Directory.

## <a name="overview"></a>Información general
Cloud App Discovery es una característica de Azure AD y se hospeda en Microsoft Azure.  
agente de extremo de Cloud App Discovery de Hello es toocollect usa datos de detección de aplicación desde equipos de TI administrados.  
Hello los datos recopilados se envían de forma segura a través de un servicio de Azure AD Cloud App Discovery toohello de canal cifrado.  
Hola datos de Cloud App Discovery de una organización, a continuación, es visible en hello portal de Azure. 

![Funcionamiento de Cloud App Discovery](./media/active-directory-cloudappdiscovery-security-and-privacy-considerations/cad01.png) 

Hello las secciones siguientes siguen Hola flujo de información y describen cómo se protege a medida que se mueven desde el servicio de Cloud App Discovery de toohello de organización y, en última instancia, el portal de Cloud App Discovery toohello.

## <a name="collecting-data-from-your-organization"></a>Recopilación de datos de su organización
En aplicación de nube detección característica tooget información de orden toouse Azure Active Directory sobre Hola aplicaciones usadas los empleados de su organización, debe toofirst implementar hello Azure AD Cloud App Discovery endpoint agent toomachines en su organización.

Los administradores del inquilino de Azure Active Directory hello (o su delegado) pueden descargar el paquete de instalación del agente de Hola de hello portal de Azure. agente de Hello puede manualmente instalado o instalarse en varios equipos en la organización de hello mediante SCCM o la directiva de grupo.

Para obtener más instrucciones sobre las opciones de implementación, consulte la [Guía de implementación de directivas de grupo de Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30965.cloud-app-discovery-group-policy-deployment-guide.aspx).


### <a name="data-collected-by-hello-agent"></a>Datos recopilados por el agente de Hola
Cuando se realiza una conexión tooa aplicación Web, se recopila información de Hola que se describen en la siguiente lista de hello agente Hola. Hello información se recopila solo para aquellas aplicaciones que Administrador de hello ha configurado para la detección.  
Puede editar lista de Hola de las aplicaciones de nube que Hola monitores de agente a través de la hoja de Cloud App Discovery de Hola Hola Microsoft [portal de Azure](https://portal.azure.com/), en **configuración**->**datos Colección**->**lista de la colección de aplicaciones**. Para obtener más información, consulte [Introducción a Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)


**Información de categoría**: información de usuario  
**Descripción**:  
nombre de usuario de Windows Hello del proceso de hello realizados por una aplicación Web de destino de solicitud toohello (p. ej.: dominio ombre de usuario), así como el identificador de seguridad de Windows (SID) del usuario de Hola Hola.

**Categoría de información**: información de proceso  
**Descripción**:  
nombre de Hello del proceso de Hola que realizan la aplicación Web de hello solicitud toohello destino (p. ej.: "iexplore.exe")

**Categoría de información**: información de la máquina  
**Descripción**:  
nombre de NetBIOS de máquina de Hello en qué Hola agente está instalado.

**Categoría de información**: información de tráfico de aplicaciones  
**Descripción**: 

Hola siguiendo la información de conexión:

* origen de Hello (equipo local) y direcciones IP de destino y números de puerto
* dirección IP pública de Hola de organización de Hola a través de qué Hola solicitud sale.
* tiempo de saludo de solicitud de Hola
* volumen de Hola de tráfico enviados y recibidos
* versión IP de Hello (4 o 6)
* Para las conexiones TLS sólo: nombre de host de destino de hello del certificado de servidor de Hola o de extensiones de indicación de nombre de servidor de Hola.

Hola la siguiente información de HTTP:

* Método (GET, POST, etc.).
* Protocolo (HTTP/1.1, etc.).
* Cadena de agente de usuario
* Nombre de host.
* URI de destino (sin incluir la cadena de consulta).
* Información del tipo de contenido.
* Información de dirección URL del origen de referencia (sin incluir la cadena de consulta).

> [!NOTE]
> Hola información HTTP anterior se recopila para todas las conexiones no cifradas.
> Para las conexiones TLS, esta información se captura solo cuando hello 'Inspección profunda' esté activada en el portal de Hola. saludo es 'ON' de forma predeterminada.
> Para obtener más información, vea a continuación y consulte [Introducción a Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)
> 
> 

Además toohello datos que el agente Hola recopila acerca de la actividad de red de hello, también recopila información anónima sobre la configuración de hardware y software de hello, informes de errores y obtener información acerca de cómo se utiliza el agente de Hola.


### <a name="how-hello-agent-works"></a>Cómo funciona el agente de Hola
instalación del agente Hola incluye dos componentes:

* Un componente de modo de usuario
* Un componente de controlador de modo kernel (controlador de Plataforma de filtrado de Windows)

Cuando se instala por primera vez agente Hola almacena un certificado de confianza específicas del equipo en la máquina de Hola donde, a continuación, utiliza tooestablish una conexión segura con el servicio de Cloud App Discovery de Hola.  
agente Hola periódicamente recupera la configuración de directiva de hello servicio Cloud App Discovery a través de esta conexión segura.  
Directiva de Hello incluye información sobre qué toomonitor de aplicaciones de nube y si la actualización automática debe habilitarse, entre otras cosas.

Como el tráfico Web se enviados y recibido en la máquina de Hola desde Internet Explorer y Chrome, agente de Cloud App Discovery de hello analiza el tráfico de Hola y extrae Hola metadatos relevantes (vea hello **datos recopilados por el agente de hello** sección la parte superior).  
Cada minuto, agente de hello carga Hola recopilan metadatos toohello servicio Cloud App Discovery a través de un canal cifrado.

intercepta de componente de controlador de Hola Hola tráfico no cifrado y se inserta en la secuencia cifrada Hola. Para obtener más detalles en hello **interceptar datos de las conexiones cifradas (la inspección en profundidad)** sección más adelante.

### <a name="respecting-user-privacy"></a>Respeto de la privacidad de los usuarios
Nuestro objetivo es tooprovide administradores Hola herramientas tooset Hola equilibrio entre la óptica detallada en privacidad de uso y de usuario de aplicación según corresponda para su organización. final de toothat, proporcionamos Hola siguientes botones en la página de configuración de Hola Hola Portal:

* **Recopilación de datos**: los administradores pueden elegir toospecify qué aplicaciones o categorías de la aplicación en la que quiere tooget detección datos.
* **La inspección en profundidad**: los administradores puede elegir toospecify si el agente de hello recopile tráfico HTTP para conexiones SSL/TLS (también conocido como **'Inspección profunda'**). Más información sobre esto en la sección siguiente Hola.
* **Opciones de consentimiento**: los administradores pueden usar Hola Cloud App Discovery portal toochoose si los usuarios toonotify Hola de recopilación de datos por agente hello, y si el usuario de toorequire dar su consentimiento antes de que el agente de hello empieza a recopilar datos de usuario.

agente de punto de conexión de Hello Cloud App Discovery solo recopila información de hello descrito en hello **datos recopilados por el agente de hello** sección anterior.

### <a name="intercepting-data-from-encrypted-connections-deep-inspection"></a>Interceptación de datos de conexiones cifradas (inspección en profundidad)
Como mencionamos anteriormente, los administradores pueden configurar datos de toomonitor de agente de saludo de conexiones cifradas ('inspección profunda'). TLS ([Transport Layer Security](https://msdn.microsoft.com/library/windows/desktop/aa380516%28v=vs.85%29.aspx)) es uno de hello protocolos más comunes en uso en hello Internet hoy en día. Al cifrar la comunicación con TLS, un cliente puede establecer un canal de comunicación segura y privada con un servidor web; TLS proporciona una protección esencial para pasar las credenciales de autenticación y evitar la divulgación de Hola de información confidencial.

Mientras hello-to-end segura canal cifrado TLS proporcionada habilita la protección de la privacidad y seguridad importantes, a menudo es abusen del protocolo de hello con fines malintencionados o malintencionadas. Sea tan por lo tanto, de hecho, que a menudo es TLS conocen tooas Hola "omisión de firewall universal protocolo". raíz Hola de problema de hello es que la mayoría de los servidores de seguridad son comunicación TLS de tooinspect no se puede porque los datos de la capa de aplicación de hello está cifrados con SSL. Sabiendo esto, los atacantes aprovechan con frecuencia usuario de tooa TLS toodeliver cargas malintencionado segura de que incluso hello más capas de la aplicación los firewalls inteligentes son completamente oculta tooTLS y simplemente deben transmitir la comunicación TLS entre hosts. Con frecuencia, los usuarios finales aprovechar controles de acceso de toobypass TLS aplicados sus servidores proxy, usar a tooconnect toopublic proxy y firewalls corporativos y para protocolos no TLS a través de firewall de Hola que en caso contrario, puede estar bloqueado por la directiva de túnel.

La inspección en profundidad permite tooact de agente de Cloud App Discovery de hello como una confianza man-in-the-middle. Cuando se realiza una solicitud de cliente tooaccess HTTPS al recurso protegido, controlador de agente de punto de conexión de hello intercepta conexión hello y establece un tooretrieves de servidor de destino de nueva conexión toohello su propio certificado SSL en nombre del cliente de Hola. agente de Hello, a continuación, comprueba que Hola certificado puede ser de confianza (mediante la comprobación de que no se ha revocado y realizar otras comprobaciones de certificado), y si se superan estos, hello agente de punto de conexión, a continuación, copia la información de Hola de certificado de servidor de Hola y crea su propio certificado de servidor, conocido como un certificado de interceptación--con esa información. certificado de intercepción de Hello está firmada marcha por agente de punto de conexión de hello con un certificado raíz, que está instalado en el almacén de certificados de confianza de Windows hello. Este certificado raíz autofirmado está marcada como no exportable y es ACL tenía tooadministrators. Es toonever previsto deje Hola máquina en la que se creó. Cuando la aplicación de cliente de saludo del usuario final reciba el certificado de interceptación de hello, confíe en él porque correctamente puede validar la cadena de certificados de hello todos los certificados de raíz de toohello de manera Hola. Este proceso resulta casi transparente desde el punto de vista del usuario final con algunas salvedades que se describen a continuación.

Habilitando la inspección en profundidad, Hola Cloud App Discovery Endpoint Agent puede descifrar e inspeccionar las comunicaciones de TLS cifrados, permitiendo ruido de tooreduce de servicio de Hola y proporcionan información sobre el uso de Hola de aplicaciones en la nube Hola cifrado.

#### <a name="a-word-of-caution"></a>Unas palabras de advertencia
Antes de activar la inspección en profundidad, se recomienda encarecidamente que se comunican sus intenciones tooyour legal y departamentos de recursos humanos y obtener su consentimiento. La inspección de las comunicaciones cifradas privadas del usuario final pueden ser un asunto delicado, por razones obvias. Antes de una producción puesta en servicio de la inspección en profundidad, asegúrese de que la seguridad de la empresa y se han actualizado las directivas de uso aceptable se inspeccionará tooindicate que la comunicación cifrada. Notificación al usuario y exención de sitios considera confidencial (por ejemplo, operaciones bancarias y médicas) también pueden ser necesarios si configura Cloud App Discovery toomonitor ellos. Tal y como se mencionó anteriormente, los administradores pueden usar Hola Cloud App Discovery portal toochoose si los usuarios de toonotify Hola de recopilación de datos por agente hello, y si el usuario de toorequire dar su consentimiento antes de que el agente de hello empieza a recopilar datos de usuario.

### <a name="known-issues-and-drawbacks"></a>Desventajas y problemas conocidos
Hay algunos casos donde interceptación de TLS puede afectar la experiencia del usuario final hello:

* Los certificados de validación (EV) extendida representan la barra de direcciones de Hola de hello web explorador verde tooact como una pista visual que está visitando un sitio web de confianza. Inspección TLS no puede duplicar EV certificado Hola emite a toohello cliente, por lo que los sitios web que usan certificados de validación Extendida funcionarán normalmente pero barra de direcciones de hello no mostrará verde.  
* Anclaje de clave pública (también conocido como certificado de anclaje) están diseñadas toohelp proteger a los usuarios frente a ataques de man-in-the-middle y no autorizados entidades emisoras de certificados. Cuando el certificado de raíz de Hola para un sitio anclado no coincide con uno de hello conocida buena CA, Explorador de hello rechaza la conexión de hello con un error. Puesto que la interceptación de TLS es, de hecho, un ataque de tipo «Man in the middle», se producirá un error en estas conexiones.
* Si los usuarios haga clic en el icono de candado de hello en hello explorador dirección barra Explorador tooinspect Hola información del sitio, no verán una cadena termina en la entidad emisora de certificados de hello usa certificado de sitio Web de toosign hello, pero en su lugar, una cadena de certificados termina con Hola Windows almacén de certificados de confianza.

repeticiones de hello tooreduce de estos problemas, es realizar un seguimiento de servicios en la nube y aplicaciones cliente conocida toouse extendidos validación o anclaje de clave pública y dar instrucciones a Hola Endpoint Agent tooavoid interceptando conexiones afectadas. Incluso en estos casos, sin embargo, seguirá recibiendo informes de uso de Hola de estas aplicaciones en la nube y el volumen de Hola de datos que se transfieren, pero puesto que no son profundos inspeccionar, no hay detalles acerca de cómo se usan aplicaciones de hello estará disponibles.

## <a name="sending-data-toocloud-app-discovery"></a>Enviar datos tooCloud App Discovery
Una vez que haya recopilado los metadatos por agente hello, se almacena en caché en la máquina de Hola para tooone minuto o hasta Hola datos almacenados en caché alcanzan un tamaño de 5MB. A continuación, se comprimen y envían a través de un servicio de Cloud App Discovery toohello de conexión segura.

Si Hola agente no se puede toocommunicate con hello servicio Cloud App Discovery por algún motivo, hello metadatos recopilados se almacenan en una caché de archivos local que sólo puede tener acceso a los usuarios con privilegios en la máquina de hello (por ejemplo, el grupo de administradores de hello).  
agente de Hello automáticamente intentos tooresend Hola metadatos que están almacenados hasta que se recibieron correctamente por servicio de Cloud App Discovery de Hola.

## <a name="receiving-hello-data-at-hello-service-end"></a>Recibir datos de hello en extremo de servicio de Hola
agentes de Hello autenticar toohello Cloud App Discovery servicio mediante el certificado de autenticación de cliente específico de máquina de hello mencionada anteriormente y reenvía los datos a través de un canal cifrado.  
análisis del servicio de Cloud App Discovery de Hello canalización metadatos de procesos para cada cliente por separado realizando particiones lógicas a través de todas las fases de canalización de análisis de Hola.
Hola analiza metadatos unidades Hola varios informes en el portal de Hola.

Hola metadatos sin procesar y metadatos Hola analizado se almacenan para los días de too180. Además, los clientes pueden elegir toocapture Hola analizan metadatos en una cuenta de almacenamiento de blobs de Azure de su elección.
Esto es útil para análisis sin conexión de metadatos, así como más retención de datos de Hola.

## <a name="accessing-hello-data-using-hello-azure-portal"></a>Acceso a datos de hello con hello portal de Azure
En un esfuerzo de metadatos de la hello tookeep recopilan seguro, de forma predeterminada sólo los administradores globales del inquilino de hello tienen acceso toohello Cloud App Discovery característica Hola portal de Azure.  
Sin embargo, los administradores pueden elegir toodelegate esta tooother de acceso de los usuarios o grupos.

> [!NOTE]
> Para obtener más información, consulte [Introducción a Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)
> 
> 


Los datos de usuario al tener acceso al hello en el portal de hello, deben tener licencia con una licencia de Azure AD Premium.

## <a name="additional-resources"></a>Recursos adicionales
* [¿Cómo puedo detectar aplicaciones en la nube no sancionadas que se usan dentro de mi organización?](active-directory-cloudappdiscovery-whatis.md)
* [Índice de artículos sobre la administración de aplicaciones en Azure Active Directory](active-directory-apps-index.md)

