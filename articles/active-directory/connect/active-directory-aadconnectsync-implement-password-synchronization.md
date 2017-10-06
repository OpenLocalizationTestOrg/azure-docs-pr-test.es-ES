---
title: "sincronización de contraseña de aaaImplement con sincronización de Azure AD Connect | Documentos de Microsoft"
description: "Proporciona información acerca de cómo funciona la sincronización de contraseña y cómo tooset seguridad."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 05f16c3e-9d23-45dc-afca-3d0fa9dbf501
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: billmath
ms.openlocfilehash: a0401640f2a4d914419ee4446f923bb3a972389d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="implement-password-synchronization-with-azure-ad-connect-sync"></a>Implementación de la sincronización de contraseña mediante la sincronización de Azure AD Connect
Este artículo proporciona información que necesita toosynchronize las contraseñas de usuario desde una instancia local de Active Directory instancia tooa basada en la nube Azure Active Directory (Azure AD).

## <a name="what-is-password-synchronization"></a>Qué es la sincronización de contraseñas
Hola probabilidad relacionados con la que está bloqueada entre el trabajo realizado debido tooa olvidado contraseña toohello número de contraseñas diferentes que necesita tooremember. Hola más contraseñas necesita tooremember, Hola superior Hola probabilidad tooforget uno. Preguntas y llamadas sobre los restablecimientos de contraseña y otras petición problemas relacionados con la contraseña Hola mayoría de los recursos de soporte técnico.

Sincronización de contraseñas es que una característica usa contraseñas de usuario de toosynchronize desde una instancia de tooa basada en la nube de Azure AD de instancia de Active Directory local.
Utilice esta característica toosign en servicios de tooAzure AD como Office 365, Microsoft Intune, CRM Online y Azure Active Directory Domain Services (Azure AD DS). Iniciar sesión en el servicio de toohello mediante el uso de hello misma contraseña que usa toosign en tooyour local instancia de Active Directory.

![Qué es Azure AD Connect](./media/active-directory-aadconnectsync-implement-password-synchronization/arch1.png)

Al reducir el número de Hola de contraseñas, los usuarios necesitan toojust toomaintain uno. La sincronización de contraseña le ayuda a:

* Mejorar la productividad de Hola de los usuarios.
* Reducir los costos de soporte técnico.  

Además, si decide toouse [federación con los servicios de federación de Active Directory (AD FS)](https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Configuring-AD-FS-for-user-sign-in-with-Azure-AD-Connect), opcionalmente puede configurar la sincronización de contraseña como una copia de seguridad en caso de que se produce un error en la infraestructura de AD FS.

Sincronización de contraseñas es una característica de sincronización de directorio de extensión toohello implementada por la sincronización de Azure AD Connect. sincronización de contraseña de toouse en su entorno, debe:

* Instalar Azure AD Connect.  
* Configure la sincronización de directorios entre su instancia de Active Directory local y la de Azure Active Directory.
* Habilitar la sincronización de contraseña.

Para más información, consulte [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).

> [!NOTE]
> Para obtener más información sobre Azure Active Directory Domain Services configurado para la sincronización de contraseña y FIPS, vea "Sincronización de contraseñas y FIPS" más adelante en este artículo.
>
>

## <a name="how-password-synchronization-works"></a>Funcionamiento de la sincronización de contraseñas
Hola servicios de dominio de Active Directory almacena contraseñas en forma de Hola de una representación del valor de hash de contraseña de usuario real de Hola. Un valor hash es el resultado de una función matemática unívoca (hello *algoritmo hash*). No hay ningún método toorevert Hola dar lugar a una versión de texto sin formato toohello función unidireccional de una contraseña. No puede usar un toosign de hash de contraseña de red de tooyour local.

toosynchronize su contraseña, Azure AD Connect sync extrae el hash de contraseña de Hola instancia local de Active Directory. Se aplica un procesamiento adicional de seguridad toohello hash de contraseña antes de que sincroniza toohello servicio de autenticación de Azure Active Directory. Las contraseñas se sincronizan usuario por usuario y en orden cronológico.

flujo de datos real de Hello del proceso de sincronización de contraseña de hello es similar toohello sincronización de datos de usuario como nombre para mostrar o direcciones de correo electrónico. Sin embargo, las contraseñas se sincronizan con mayor frecuencia que la ventana de sincronización de directorios estándar de hello para otros atributos. proceso de sincronización de contraseña de Hola se ejecuta cada 2 minutos. No se puede modificar la frecuencia de Hola de este proceso. Al sincronizar una contraseña, sobrescribe contraseña de hello existente en la nube.

Hello primera vez que habilite la característica de sincronización de contraseña de hello, realiza una sincronización inicial de las contraseñas de Hola de todos los usuarios en el ámbito. No se puede definir explícitamente un subconjunto de las contraseñas de usuario que desea toosynchronize.

Cuando se cambia una contraseña local, Hola actualizado contraseña se sincroniza, con mayor frecuencia en cuestión de minutos.
característica de sincronización de contraseña de Hello automáticamente reintenta la sincronización errónea. Si produce un error durante un intento de toosynchronize una contraseña, se registra un error en el Visor de eventos.

sincronización de Hola de una contraseña no influye en usuario de Hola que actualmente ha iniciado sesión.
La sesión actual del servicio de nube no está afectada inmediatamente por un cambio de contraseña sincronizada que tiene lugar mientras se firman tooa del servicio en nube. Sin embargo, al servicio en la nube Hola requiere que tooauthenticate nuevo, deberá tooprovide la nueva contraseña.

Un usuario debe introducir sus credenciales corporativos un segundo tooAzure de tooauthenticate tiempo AD, independientemente de si has iniciado sesión en la red corporativa de tootheir. Puede minimizar estos patrón, sin embargo, si el usuario de hello selecciona Hola tenga iniciada en la casilla de verificación (KMSI) en Inicio de sesión. Con esta activación se establece una cookie de sesión que omite la autenticación durante un breve período. Comportamiento KMSI se puede habilitar o deshabilitar Administrador de Azure AD Hola.

> [!NOTE]
> Solo se admite la sincronización de contraseñas de usuario de tipo de objeto de hello en Active Directory. No se admite para el tipo de objeto iNetOrgPerson Hola.

### <a name="detailed-description-of-how-password-synchronization-works"></a>Descripción detallada de cómo funciona la sincronización de contraseña
Hola a continuación describe detallada cómo funciona la sincronización de contraseña entre Active Directory y Azure AD.

![Flujo detallado de contraseñas](./media/active-directory-aadconnectsync-implement-password-synchronization/arch3.png)


1. Cada dos minutos, agente de sincronización de contraseña de hello en servidor de hello AD Connect solicita hashes de contraseña almacenada (atributo de unicodePwd Hola) desde un controlador de dominio a través de hello estándar [MS-drsr a](https://msdn.microsoft.com/library/cc228086.aspx) protocolo de replicación utiliza datos toosynchronize entre los controladores de dominio. cuenta de servicio de Hello debe tener replicar cambios de directorio y replicar Directory cambios, todos AD hashes de contraseña de Hola de tooobtain permisos (se conceden de manera predeterminada en la instalación).
2. Antes de enviar, Hola DC cifra hash de contraseña de hello MD4 mediante una clave que es un [MD5](http://www.rfc-editor.org/rfc/rfc1321.txt) hash de clave de sesión RPC de Hola y un valor "salt". A continuación, envía a agente de sincronización de contraseña de hello resultado toohello a través de RPC. Hola DC también pasa a agente de sincronización de hello toohello "salt" con el protocolo de replicación de Hola DC, por lo que el agente de hello será toodecrypt capaz de sobres de Hola.
3.  Después de agente de sincronización de contraseña de hello tiene sobre codificado hello, usa [MD5CryptoServiceProvider](https://msdn.microsoft.com/library/System.Security.Cryptography.MD5CryptoServiceProvider.aspx) y Hola toogenerate "salt" formato original MD4 en toodecrypt clave Hola recibido datos tooits atrás. En ningún momento tiene agente de sincronización de contraseña de hello acceso toohello contraseña sin cifrado. Hello uso del agente de sincronización de contraseña de MD5 es estrictamente para la compatibilidad de protocolo de replicación con hello DC, y solo se utiliza de forma local entre Hola DC y agente de sincronización de contraseña de Hola.
4.  agente de sincronización de contraseña de Hello amplía bytes de too64 de hash de contraseña binarios de 16 bytes de hello al primer convertir Hola hash tooa 32 bytes cadena hexadecimal, a continuación, convertir esta cadena de nuevo en binario con codificación UTF-16.
5.  agente de sincronización de contraseña de Hello agrega un valor "salt", que consta de un valor "salt" longitud de 10 bytes, toofurther binario de 64 bits de toohello proteger hash original Hola.
6.  agente de sincronización de contraseña de Hello, a continuación, combina hash MD4 hello más valor "salt" e introduce en hello [PBKDF2](https://www.ietf.org/rfc/rfc2898.txt) función. 1000 iteraciones de hello [HMAC-SHA256](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) se utiliza el algoritmo hash con clave. 
7.  agente de sincronización de contraseña de Hello toma el hash de 32 bytes resultante hello, concatena dos valor "salt" Hola y Hola número de SHA256 iteraciones tooit (para su uso con Azure AD) y transmite la cadena Hola de Azure AD Connect tooAzure AD a través de SSL.</br> 
8.  Cuando un usuario intenta toosign en tooAzure AD y escribe su contraseña, una contraseña de Hola se ejecutan a través de hello MD4 mismo + "salt" + PBKDF2 + HMAC-SHA256 proceso. Si hash resultante Hola coincide con hash Hola almacenada en Azure AD, usuario Hola especificó la contraseña correcta de Hola y se autentica. 

>[!Note] 
>algoritmo hash MD4 original de Hello no es tooAzure transmitido AD. En su lugar, se transmite Hola hash SHA256 del algoritmo hash MD4 original Hola. Como resultado, si se obtiene el hash de hello almacenada en Azure AD, no se pueden utilizar en un ataque de pass-the-hash en local.

### <a name="how-password-synchronization-works-with-azure-active-directory-domain-services"></a>Funcionamiento de la sincronización de contraseñas con Azure Active Directory Domain Services
También puede utilizar toosynchronize de característica de sincronización de contraseña de hello las contraseñas locales demasiado[servicios de dominio de Active Directory de Azure](../../active-directory-domain-services/active-directory-ds-overview.md). En este escenario, instancia de servicios de dominio de Active Directory de Azure Hola autentica los usuarios en la nube de hello con todos los métodos de hello disponibles en la instancia local de Active Directory. experiencia de Hola de este escenario es similar hello toousing herramienta de migración de Active Directory (ADMT) en un entorno local.

### <a name="security-considerations"></a>Consideraciones sobre la seguridad
Al sincronizar contraseñas, versión de texto sin formato de saludo de la contraseña no es característica de sincronización de contraseña toohello expuesto, tooAzure AD o cualquiera de los servicios de hello asociado.

Autenticación de usuario tiene lugar en Azure AD, en lugar de en la instancia de Active Directory de la organización de Hola. Si su organización tiene preocupaciones sobre datos de contraseña en cualquier formato dejando Hola local, tenga en cuenta hechos Hola ese Hola SHA256 datos de contraseñas almacenados en Azure AD--un hash del algoritmo hash MD4 original Hola--es mucho más segura que el contenido almacenado en Active Directory. Además, porque no se puede descifrar este hash SHA256, no se vuelve al entorno de Active Directory de la organización toohello y presenta como una contraseña de usuario válido en un ataque pass-the-hash.





### <a name="password-policy-considerations"></a>Consideraciones de la directiva de contraseña
Existen dos tipos de directivas de contraseña que se ven afectados por la habilitación de la sincronización de contraseñas:

* Directiva de complejidad de contraseñas
* Directiva de expiración de contraseñas

#### <a name="password-complexity-policy"></a>Directiva de complejidad de contraseñas  
Cuando se habilita la sincronización de contraseña, directivas de complejidad de contraseña de hello en la instancia de Active Directory local anulan las directivas de complejidad en la nube de Hola para los usuarios sincronizados. Puede usar todas Hola válido contraseñas de la instancia de Active Directory local tooaccess servicios de Azure AD.

> [!NOTE]
> Las contraseñas para los usuarios que se crean directamente en la nube de hello siguen siendo tal como se define en la nube de hello las directivas de toopassword de asunto.

#### <a name="password-expiration-policy"></a>Directiva de expiración de contraseñas  
Si un usuario está en ámbito de Hola de sincronización de contraseña, la contraseña de la cuenta de hello en la nube se establece demasiado*no Expire nunca*.

Puede continuar toosign en servicios en la nube tooyour mediante una contraseña sincronizada que ha expirado en su entorno local. Se actualiza la contraseña en la nube Hola la próxima vez que cambia la contraseña de hello en entorno local de Hola.

#### <a name="account-expiration"></a>Expiración de la cuenta
Si su organización usa el atributo de hello accountExpires como parte de la administración de cuentas de usuario, tenga en cuenta que este atributo no está sincronizada tooAzure AD. Por consiguiente, una cuenta de Active Directory expirada en un entorno configurado para la sincronización de contraseña seguirá activa en Azure AD. Se recomienda que, si la cuenta de hello ha expirado, una acción de flujo de trabajo debe desencadenar un script de PowerShell que deshabilita la cuenta de Azure AD del usuario de Hola. Por el contrario, cuando se activa la cuenta de hello, instancia de Azure AD Hola debe estar activado.

### <a name="overwrite-synchronized-passwords"></a>Sobrescritura de las contraseñas sincronizadas
Un administrador puede restablecer manualmente la contraseña mediante Windows PowerShell.

En este caso, nueva contraseña de hello invalida su contraseña sincronizada, y todas las directivas de contraseñas definidas en la nube de hello son aplicados toohello nueva contraseña.

Si cambia la contraseña local nuevo, Hola nueva contraseña es sincronizado toohello en la nube, y reemplaza contraseña Hola actualizado manualmente.

sincronización de Hola de una contraseña no influye en hello Azure usuario que ha iniciado sesión. La sesión actual del servicio de nube no está afectada inmediatamente por un cambio de contraseña sincronizada que tiene lugar mientras ha iniciado sesión en el servicio en la nube tooa. KMSI amplía esta diferencia de tiempo que dure Hola. Al servicio en la nube Hola requiere que tooauthenticate nuevo, deberá tooprovide la nueva contraseña.

### <a name="additional-advantages"></a>Ventajas adicionales

- Por lo general, la sincronización de contraseña es más sencillo tooimplement que un servicio de federación. No requiere ningún servidor adicionales y elimina la dependencia de a los usuarios tooauthenticate de servicio de federación de alta disponibilidad. 
- Sincronización de contraseña también puede habilitarse en toofederation de adición. Puede usarse como reserva en caso de que el servicio de federación experimente una interrupción del servicio.












## <a name="enable-password-synchronization"></a>Habilitación de la sincronización de contraseñas
Cuando se instala Azure AD Connect con hello **configuración rápida** opción, la sincronización de contraseña se habilita automáticamente. Para conocer más detalles, consulte [Introducción a Azure AD Connect mediante la configuración rápida](active-directory-aadconnect-get-started-express.md).

Si utiliza una configuración personalizada al instalar Azure AD Connect, sincronización de contraseñas está disponible en la página de inicio de sesión de usuario de Hola. Para más información, consulte [Instalación personalizada de Azure AD Connect](active-directory-aadconnect-get-started-custom.md).

![Habilitación de la sincronización de contraseñas](./media/active-directory-aadconnectsync-implement-password-synchronization/usersignin.png)

### <a name="password-synchronization-and-fips"></a>Sincronización de contraseñas y FIPS
Si el servidor se ha bloqueado según tooFederal Information Processing Standard (FIPS), se deshabilita MD5.

**tooenable MD5 para la sincronización de contraseña, lleve a cabo Hola pasos:**

1. Vaya too%programfiles%\Azure AD Sync\Bin.
2. Abra miiserver.exe.config.
3. Vaya toohello configuration/runtime nodo final Hola del archivo hello.
4. Agregue Hola siguiente nodo:`<enforceFIPSPolicy enabled="false"/>`
5. Guarde los cambios.

Como referencia, este fragmento de código debe ser similar al siguiente:

```
    <configuration>
        <runtime>
            <enforceFIPSPolicy enabled="false"/>
        </runtime>
    </configuration>
```

Para obtener información sobre la seguridad y FIPS, vea [AAD Password Sync, Encryption and FIPS compliance](https://blogs.technet.microsoft.com/enterprisemobility/2014/06/28/aad-password-sync-encryption-and-fips-compliance/) (Cumplimiento de sincronización de contraseña, cifrado y FIPS AAD).

## <a name="troubleshoot-password-synchronization"></a>Solución de problemas de sincronización de contraseñas
Si tiene problemas con la sincronización de contraseña, vea [Solución de problemas de sincronización de contraseñas](active-directory-aadconnectsync-troubleshoot-password-synchronization.md).

## <a name="next-steps"></a>Pasos siguientes
* [Sincronización de Azure AD Connect: personalización de las opciones de sincronización](active-directory-aadconnectsync-whatis.md)
* [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md)
