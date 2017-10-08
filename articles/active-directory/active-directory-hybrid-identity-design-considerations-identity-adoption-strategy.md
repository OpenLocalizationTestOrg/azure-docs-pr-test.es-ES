---
title: "Consideraciones de diseño de identidad de aaaAzure Active Directory híbrida - definir una estrategia de adopción de identidad híbrida | Documentos de Microsoft"
description: "Con control de acceso condicional, Azure Active Directory comprueba las condiciones específicas de Hola que elegir al autenticar usuario hello y antes de permitir el acceso toohello aplicación. Una vez que se cumplen estas condiciones, usuario de hello es autenticado y acceso toohello aplicación permitida."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: b92fa5a9-c04c-4692-b495-ff64d023792c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 9ffca675d0c714392adfcbbc4dcfad12fccbac78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="define-a-hybrid-identity-adoption-strategy"></a>Definición de una estrategia de adopción de identidad híbrida
En esta tarea, definirá la estrategia de adopción de identidad híbrida de Hola para sus híbrida identidad solución toomeet Hola requisitos empresariales que se trataron en:

* [Determinación de las necesidades empresariales](active-directory-hybrid-identity-design-considerations-business-needs.md)
* [Determinación de los requisitos de sincronización de directorios](active-directory-hybrid-identity-design-considerations-directory-sync-requirements.md)
* [Determinación de los requisitos de autenticación multifactor](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md)

## <a name="define-business-needs-strategy"></a>Definición de una estrategia de necesidades empresariales
primera tarea de Hello enfrenta necesidades del negocio de organizaciones de hello determinantes.  Dicha tarea puede ser muy amplia y se puede producir un arrastramiento del alcance si no se tiene cuidado.  En principio Hola simplificarlo, pero recuerde que siempre tooplan para lograr un diseño que va a alojar y facilitar el cambio en el futuro de Hola.  Independientemente de si es un diseño sencillo o un archivo muy complejos, Azure Active Directory es la plataforma de Microsoft Identity de Hola que es compatible con Office 365, Microsoft Online Services y aplicaciones de nube.

## <a name="define-an-integration-strategy"></a>Definición de una estrategia de integración
Microsoft tiene tres escenarios de integración principales que son las identidades de nube, las identidades sincronizadas y las identidades federadas.  Debe planear la adopción de una de estas estrategias de integración.  Hola estrategia que elija puede variar y pueden incluir las decisiones de hello en la elección de una, qué tipo de experiencia del usuario que desee tooprovide, ¿tiene parte de la infraestructura existente de hello ya en el contexto y lo que es más rentable de hello.  

![](./media/hybrid-id-design-considerations/integration-scenarios.png)

escenarios de Hello definidos en hello por encima de la ilustración son:

* **Las identidades de nube**: se trata de identidades que residen únicamente en la nube de Hola.  En caso de hello de Azure AD, ¿residen específicamente en su directorio Azure AD.
* **Sincronizar**: se trata de identidades que hay en el sistema local y en la nube de Hola.  Con Azure AD Connect, los usuarios se crean o se conectan con las cuentas de Azure AD existentes.  Hello se sincroniza hash de contraseña del usuario de nube de toohello de entorno de hello local en lo que se conoce como un hash de contraseña.  Al usar sincronizado una advertencia de hello es que si un usuario está deshabilitado en el entorno local de hello, pueden tardar horas too3 para ese tooshow de estado de la cuenta de Azure AD.  Esto es debido a toohello intervalo de tiempo de sincronización.
* **Federado**: estas identidades existen tanto en forma local y en la nube de Hola.  Con Azure AD Connect, los usuarios se crean o se conectan con las cuentas de Azure AD existentes.  

> [!NOTE]
> Para obtener más información acerca de las opciones de sincronización de hello leer [integrar las identidades locales con Azure Active Directory](connect/active-directory-aadconnect.md).
> 
> 

Hello en la tabla siguiente le ayudará a determinar Hola ventajas y desventajas de cada uno de hello siguientes estrategias:

| Estrategia | Ventajas | Desventajas |
| --- | --- | --- |
| **Identidades en la nube** |Toomanage más fácil para pequeñas empresas. <br> No necesita hardware adicional de tooinstall No en local<br>Deshabilitar fácilmente si el usuario de hello deja la empresa de Hola |Los usuarios necesitarán en toosign al tener acceso a las cargas de trabajo en la nube de Hola <br> Las contraseñas pueden o no ser igual Hola para identidades de nube y locales |
| **Sincronizada** |La contraseña local se autenticará localmente y en directorios en la nube. <br>Toomanage más fácil para organizaciones pequeñas, medianas o grandes <br>Los usuarios pueden tener el inicio de sesión único (SSO) en algunos recursos. <br> Método preferido de Microsoft para la sincronización <br> Toomanage más fácil |Algunos clientes pueden ser reacios toosynchronize sus directorios con hello en la nube debido policía específicos de la empresa |
| **Federada** |Los usuarios pueden tener el inicio de sesión único (SSO). <br>Si un usuario se finaliza o se deja, cuenta de hello puede estar deshabilitada inmediatamente y se revoca el acceso,<br> Admite escenarios avanzados que no se pueden lograr con la sincronizada. |Los pasos más toosetup y configurar <br> Mayor mantenimiento <br> Puede requerir hardware adicional para la infraestructura de STS Hola <br> Puede requerir el servidor de federación de hello tooinstall de hardware adicional. Es necesario software adicional si se usa AD FS <br> Necesita una configuración amplia de SSO. <br> Crítico el punto de error si el servidor de federación de hello está inactivo, los usuarios no podrán tooauthenticate |

### <a name="client-experience"></a>Experiencia del cliente
estrategia de Hola que usas determinará la experiencia de inicio de sesión del usuario de Hola.  Hello en las tablas siguientes proporcionan información sobre qué usuarios Hola deben esperar su inicio de sesión en experimenta toobe.  Tenga en cuenta que no todos los proveedores de identidades federadas admiten SSO en todos los escenarios.

**Aplicaciones de red privada y conectadas a un dominio**:

|  | Identidad sincronizada | Identidad federada |
| --- | --- | --- |
| Exploradores web |Autenticación basada en formularios |inicio de sesión único en, a veces requiere toosupply Id. de organización |
| Outlook |Se piden credenciales |Se piden credenciales |
| Skype Empresarial (Lync) |Se piden credenciales |inicio de sesión único para Lync, credenciales solicitadas para Exchange |
| SkyDrive Pro |Se piden credenciales |inicio de sesión único |
| Suscripción a Office Pro Plus |Se piden credenciales |inicio de sesión único |

**Orígenes externos o que no son de confianza**:

|  | Identidad sincronizada | Identidad federada |
| --- | --- | --- |
| Exploradores web |Autenticación basada en formularios |Autenticación basada en formularios |
| Outlook, Skype Empresarial (Lync), Skydrive Pro, suscripción de Office |Se piden credenciales |Se piden credenciales |
| Exchange ActiveSync |Se piden credenciales |inicio de sesión único para Lync, credenciales solicitadas para Exchange |
| Aplicaciones móviles |Se piden credenciales |Se piden credenciales |

Si ha determinado de la tarea 1, que tiene un 3rd IdP o son toouse continuo de terceros una federación tooprovide con Azure AD, necesita toobe consciente de hello después admite capacidades:

* Cualquier proveedor de SAML 2.0 que es compatible con hello perfil SP-Lite admite la autenticación tooAzure AD y aplicaciones asociadas
* Admite la autenticación pasiva, lo que facilita la autenticación tooOWA, SPO, etcetera.
* Admite clientes de Exchange Online a través de hello perfil de cliente mejorado de SAML 2.0 (ECP)

También debe conocer las capacidades que no estarán disponibles:

* Sin la compatibilidad con WS-Trust o Federación, los restantes clientes activos se interrumpirán
  * Esto no significa que ningún cliente de Lync, el cliente de OneDrive, suscripción de Office, Office Mobile anterior tooOffice 2016
* Transición de la autenticación de Office toopassive le permitan toosupport puro SAML 2.0 IdPs pero soporte seguirá estando en una función del cliente por cliente

> [!NOTE]
> Hola lista más actualizada lee Hola artículo http://aka.ms/ssoproviders.
> 
> 

## <a name="define-synchronization-strategy"></a>Definición de una estrategia de sincronización
En esta tarea definirá herramientas Hola que serán local datos toohello en la nube usado toosynchronize Hola organización y qué topología debe usar.  Porque la mayoría de las organizaciones utilizan Active Directory, se proporciona información sobre el uso de preguntas de Hola de Azure AD Connect tooaddress anteriores con más detalle.  Para entornos que no tiene Active Directory, no hay información sobre el uso de FIM 2010 R2 o toohelp de MIM 2016 planear esta estrategia.  Sin embargo, las versiones futuras de Azure AD Connect admitirá directorios LDAP, así que, dependiendo de la escala de tiempo, esta información puede ser capaz de tooassist.

### <a name="synchronization-tools"></a>Herramientas de sincronización
En años de hello, varias herramientas de sincronización tienen existía y se utilizan para varios escenarios.  Actualmente, Azure AD Connect se Hola vaya tootool de elección para todos los escenarios admitidos.  AAD Sync y DirSync se siguen usando, e incluso puede que se encuentren en su entorno ahora. 

> [!NOTE]
> Para hello información más reciente sobre Hola admitida capacidades de cada herramienta, lea [comparación de herramientas de integración de directorios](active-directory-hybrid-identity-design-considerations-tools-comparison.md) artículo.  
> 
> 

### <a name="supported-topologies"></a>Topologías admitidas
Al definir una estrategia de sincronización, debe determinarse topología Hola que se utiliza. Función hello información que se determinó en el paso 2 se puede determinar qué topología es uno toouse adecuado de Hola. bosque único de Hello, solo es hello más comunes y consta de un único bosque de Active Directory y una única instancia de Azure AD de topología de AD de Azure.  Esto queda toobe utilizado en la mayoría de escenarios de Hola y topología de hello esperada cuando se utiliza la instalación de Express conectarse de Azure AD como se muestra en la siguiente ilustración de Hola.

![](./media/hybrid-id-design-considerations/single-forest.png)Único bosque escenario es muy común para las organizaciones grandes y pequeñas incluso toohave varios bosques, tal como se muestra en la figura 5.

> [!NOTE]
> Para obtener más información acerca de Hola local diferente y topologías de Azure AD con Azure AD Connect sync leen el artículo de hello [topologías para Azure AD Connect](connect/active-directory-aadconnect-topologies.md).
> 
> 

![](./media/hybrid-id-design-considerations/multi-forest.png) 

Escenario de bosques múltiples

Si este caso Hola Hola, a continuación, varios bosques única topología de Azure AD debe considerarse si hello elementos siguientes son ciertas:

* Los usuarios tienen solo 1 identidad en todos los bosques: Hola identifica de forma única sección de usuarios a continuación describe con más detalle.
* Hola usuario autentica en el que se encuentra su identidad de bosque de toohello
* Tanto el UPN como el delimitador de origen (identificador inmutable) procederán de este bosque
* Todos los bosques son accesibles, Azure AD Connect: Esto significa que no es necesario Unidos a un dominio de toobe y puede colocarse en una red Perimetral si esto facilita esto.
* Los usuarios tienen un solo buzón.
* bosque de Hola que hospeda el buzón de un usuario tiene Hola mejor calidad de los datos para los atributos visibles en hello lista Global de direcciones (GAL) de Exchange
* Si no hay ningún buzón de usuario de Hola, entonces cualquier bosque puede ser toocontribute usa estos valores
* Si tiene un buzón vinculado, a continuación, también hay otra cuenta en una toosign de otro bosque que se utiliza en.

> [!NOTE]
> Objetos que existen en tanto de forma local y en la nube de hello están "conectados" a través de un identificador único. En el contexto de Hola de sincronización de directorios, este identificador único es que se hace referencia tooas hello SourceAnchor. En contexto de Hola de Single Sign-On, esto es que se hace referencia tooas hello ImmutableId. [Conceptos de diseño de Azure AD Connect](connect/active-directory-aadconnect-design-concepts.md#sourceanchor) para obtener más información sobre el uso de Hola de SourceAnchor.
> 
> 

Si Hola anterior no son true y tiene más de una cuenta activa o más de un buzón de correo, Azure AD Connect seleccionar uno y omitir Hola otro.  Si ha vinculado los buzones de correo pero ninguna otra cuenta, estas cuentas no estará tooAzure exportado AD y que el usuario no será un miembro de los grupos.  Esto es diferente de cómo se encontraba Hola más allá con DirSync y toobetter intencional compatibilidad de estos escenarios de varios bosques. Un escenario de varios bosques se muestra en la siguiente ilustración de Hola.

![](./media/hybrid-id-design-considerations/multiforest-multipleAzureAD.png) 

**Escenario de Azure AD con bosques múltiples**

Se recomienda toohave que es simplemente un único directorio en Azure AD para una organización, pero admite que se mantiene una relación de 1:1 entre un servidor de sincronización de Azure AD Connect y un directorio de Azure AD.  En cada instancia de Azure AD, será precisa una instalación de Azure AD Connect.  Además, Azure AD, por cuestiones de diseño está aislada y los usuarios en una instancia de Azure AD no serán los usuarios pueden toosee en otra instancia.

Es posible y tooconnect admitidos una instancia de directorios de Azure AD toomultiple de Active Directory tal y como se muestra en la siguiente ilustración de hello local:

![](./media/hybrid-id-design-considerations/single-forest-flitering.png) 

**Escenario de filtrado de bosque único**

En orden toodo deben cumplirse este siguientes hello:

* Los servidores de sincronización de Azure AD Connect deben estar configurados para el filtrado, de modo que cada uno tenga un conjunto de objetos mutuamente excluyente.  Esto lo hace, por ejemplo, definir el ámbito de cada servidor tooa dominio o unidad organizativa.
* Un dominio DNS solo puede estar registrado en un único directorio de Azure AD para AD debe usar espacios de nombres independientes en local de UPN de los usuarios de Hola Hola Hola
* Los usuarios de una instancia de Azure AD solo será capaz de toosee a los usuarios de su instancia.  No puede ser usuarios de toosee capaz de Hola otras instancias
* Solo uno de los directorios de hello Azure AD puede habilitar Exchange híbrido con hello AD local
* Exclusividad mutua también se aplica toowrite back.  Esto hace que algunas de las características de la reescritura no sean compatibles con esta topología, ya que estas asumen una única configuración local.  En ella se incluye:
  * Reescritura de grupos con la configuración predeterminada
  * Reescritura de dispositivos

Tenga en cuenta que el siguiente hello no se admite y no debe elegirse como una implementación:

* No es compatible toohave varios servidores de sincronización de Azure AD Connect conectarse toohello mismo AD de Azure directory aunque estén configurado toosynchronize mutuamente conjunto del objeto de
* No se admite toosync Hola mismos directorios de Azure AD toomultiple de usuario. 
* También es un cambio de configuración a los usuarios de toomake en una tooappear de Azure AD como pone en contacto con otro directorio de Azure AD de toomake no admitido. 
* También es directorios de toomodify no admitido Azure AD Connect sync tooconnect toomultiple Azure AD.
* Los directorios de Azure AD están aislados por diseño. Es configuración de hello toochange no compatible de datos de otro directorio de Azure AD en un toobuild de tratar una GAL común y unificada entre directorios hello tooread la sincronización de Azure AD Connect. También es tooexport no compatibles a los usuarios como tooanother se pone en contacto con Azure AD Connect sync de AD local.

> [!NOTE]
> Si su organización restringe los equipos de la red impide conectarse toohello Internet, este artículo enumeran los puntos de conexión de hello (FQDN, IPv4 e IPv6 intervalos de direcciones) que se debe incluir en la salida permite listas y zona de sitios de confianza de Internet Explorer de cliente equipos tooensure los equipos correctamente pueden usar Office 365. Para obtener más información, consulte [URL de Office 365 e intervalos de direcciones IP](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2?ui=en-US&rs=en-US&ad=US).
> 
> 

## <a name="define-multi-factor-authentication-strategy"></a>Definición de una estrategia de Multi-Factor Authentication 
En esta tarea que definirá Hola toouse de estrategia de la autenticación multifactor.  Azure Multi-Factor Authentication está disponible en dos versiones diferentes.  Una está basada en nube y Hola otro es local con hello servidor Azure MFA.  Según la evaluación de hello que anterior se puede determinar qué solución es Hola uno correcto para su estrategia de.  Utilice la tabla de hello siguiente toodetermine qué opción de diseño recomendados satisfacer los requisitos de seguridad de su empresa:

Opciones de diseño multifactor:

| Toosecure activo | MFA en la nube de Hola | MFA local |
| --- | --- | --- |
| Aplicaciones de Microsoft |yes |yes |
| Aplicaciones de SaaS en Galería de aplicaciones de Hola |yes |yes |
| Aplicaciones de IIS que se publican a través del proxy de aplicación de Azure AD |yes |yes |
| Aplicaciones de IIS que no se publica a través de hello Proxy de aplicación de Azure AD |no |yes |
| Acceso remoto como VPN o RDG |no |yes |

Aunque se puede que haya decidido por una solución para su estrategia, necesitará la evaluación de hello toouse anteriores en donde se encuentran los usuarios.  Esto puede provocar Hola solución toochange.  Utilice la tabla de hello debajo tooassist que determinar esto:

| Ubicación del usuario | Opción de diseño preferida |
| --- | --- |
| Azure Active Directory |Multi-FactorAuthentication en la nube de Hola |
| Azure AD y AD local mediante la federación con AD FS |Ambos |
| Azure AD y AD local con Azure AD Connect, sin sincronización de contraseñas |Ambos |
| Azure AD y AD local con Azure AD Connect, con sincronización de contraseñas |Ambos |
| AD local |Servidor Multi-Factor Authentication |

> [!NOTE]
> También debe asegurarse de que opción de diseño de la autenticación multifactor de Hola que seleccionó admite características de Hola que son necesarios para el diseño.  Para obtener más información, lea [elegir la solución de seguridad de varios factores de hello automáticamente](../multi-factor-authentication/multi-factor-authentication-get-started.md#what-am-i-trying-to-secure).
> 
> 

## <a name="multi-factor-auth-provider"></a>Proveedor de Multi-Factor Authentication
La autenticación multifactor está disponible de forma predeterminada para los administradores globales que tienen un inquilino de Azure Active Directory. Sin embargo, si desea tooextend tooall de la autenticación multifactor de los usuarios y/o desea tooyour toobe tootake pueden utilizar características de los administradores globales como portal de administración de hello, los saludos personalizados y los informes, a continuación, debe adquirir y configurar Proveedor de la autenticación multifactor.

> [!NOTE]
> También debe asegurarse de que opción de diseño de la autenticación multifactor de Hola que seleccionó admite características de Hola que son necesarios para el diseño. 
> 
> 

## <a name="next-steps"></a>Pasos siguientes
[Determinación de los requisitos de protección de datos](active-directory-hybrid-identity-design-considerations-dataprotection-requirements.md)

## <a name="see-also"></a>Otras referencias
[Información general sobre las consideraciones de diseño](active-directory-hybrid-identity-design-considerations-overview.md)

