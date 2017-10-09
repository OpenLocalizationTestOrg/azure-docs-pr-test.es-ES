---
title: "SSPR de Azure AD con escritura diferida de contraseñas | Microsoft Docs"
description: "Con Azure AD y Azure AD Connect toowriteback contraseñas tooon-local de directory"
services: active-directory
keywords: "Administración de contraseñas de Active Directory, administración de contraseñas, autoservicio de restablecimiento de contraseña de Azure AD"
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 6a1dd964a51b4f3b5b0be303b722ab6deb4a6110
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="password-writeback-overview"></a>Información general sobre la escritura diferida de contraseñas

Escritura diferida de contraseñas permite que las contraseñas de Azure AD tooconfigure toowrite hacer tooyou Active Directory local. Quita Hola necesidad tooset seguridad y administrar una solución de restablecimiento de contraseña de autoservicio complicada en entornos, y proporciona una manera cómoda de basado en la nube para su tooreset a los usuarios sus contraseñas locales estén donde estén. La escritura diferida de contraseñas es un componente de [Azure Active Directory Connect](./connect/active-directory-aadconnect.md) que los suscriptores actuales de [Azure Active Directory Premium](active-directory-editions.md) pueden habilitar y utilizar.

Escritura diferida de contraseñas proporciona Hola después de características

* **Comentarios con retraso de cero**: la escritura diferida de contraseñas es una operación sincrónica. Los usuarios se notificación inmediatamente si su contraseña no cumple la directiva o se toobe no se puede restablecer o cambiar por cualquier motivo.
* **Admite el restablecimiento de contraseñas para usuarios que usen AD FS u otras tecnologías de federación** -con escritura diferida de contraseñas, siempre y cuando las cuentas de usuario federado hello se sincronizan una en su inquilino de Azure AD, están toomanage capaz de su AD local contraseñas de la nube de Hola.
* **Admite el restablecimiento de contraseñas de usuarios que usen [sincronizados por hash de contraseña](./connect/active-directory-aadconnectsync-implement-password-synchronization.md)**  : al servicio de restablecimiento de contraseña de hello detecta que una cuenta de usuario sincronizada está habilitada para la sincronización de hash de contraseña, restablecemos tanto esta cuenta local y la contraseña en la nube al mismo tiempo.
* **Permite cambiar las contraseñas de hello acceso panel y Office 365** : cuando federado o contraseña sincronizada toochange procedentes de los usuarios sus contraseñas expiradas o no expiradas, escribimos esos entorno tooyour atrás AD local de contraseñas.
* **Admite la escritura diferida de contraseñas cuando un administrador las restablece desde Hola portal de Azure** : cada vez que un administrador restablece una contraseña de usuario en hello [portal de Azure](https://portal.azure.com), si ese usuario es federado o sincronizados con contraseña, configuraremos Hola Hola, contraseña administrador selecciona en la instancia local de AD, también. Esto actualmente no se admite en hello Portal de administración de Office.
* **Aplica sus instalaciones en las directivas de contraseña de AD** : cuando un usuario restablece su contraseña, nos aseguramos de que cumple sus instalaciones directiva AD antes de confirmar toothat directory. Esto incluye el historial, la complejidad, la antigüedad, los filtros de contraseñas y otras restricciones de contraseña que ha definido en el entorno local de AD.
* **No requiere ninguna regla de firewall de entrada** -escritura diferida de contraseñas usa una retransmisión de Bus de servicio de Azure como canal de comunicación subyacente, lo que significa que no haya tooopen ningún puerto de entrada en el firewall para que esta característica toowork.
* **No se admite para cuentas de usuario que existen en grupos protegidos en Active Directory local**: para más información sobre grupos protegidos, vea [Cuentas protegidas y grupos de Active Directory](https://technet.microsoft.com/library/dn535499.aspx).

## <a name="how-password-writeback-works"></a>Funcionamiento de la escritura diferida de contraseñas

Cuando sincroniza un hash federado o contraseña usuario procede tooreset o cambiar su contraseña en la nube de hello, ocurre Hola siguiente:

1. Comprobamos qué tipo de usuario de contraseña hello tiene toosee.
    * Si vemos contraseña Hola se administra de forma local
        * Comprobamos si hello servicio de escritura diferida está activo y en ejecución, si lo está, dejamos usuario Hola continuar
        * Si el servicio de escritura diferida de hello no está en funcionamiento, indicamos a usuario Hola que su contraseña no se puede restablecer ahora
2. A continuación, el usuario de hello pasa puertas de autenticación adecuado de Hola y alcanza la pantalla de bienvenida restablecimiento de contraseña.
3. usuario de Hello selecciona una nueva contraseña y la confirma.
4. Al hacer clic en enviar, se cifra la contraseña de texto simple de hello con una clave simétrica que se creó durante el proceso de instalación de reescritura de Hola.
5. Después de cifrar la contraseña de hello, se incluye en una carga que se envíen a través de una retransmisión de bus del servicio específico del inquilino de tooyour de canal HTTPS (que también establecemos automáticamente durante el proceso de instalación de reescritura de hello). Esta retransmisión está protegida por una contraseña generada de forma aleatoria que sólo conoce la instalación local.
6. Una vez que llega a mensajes de bienvenida del bus de servicio, hello extremo de restablecimiento de contraseña automáticamente se reactiva y ve que tiene pendiente una solicitud de restablecimiento.
7. Hola servicio, a continuación, busca usuario hello en cuestión mediante el uso de atributo de delimitador de hello en la nube. Para este toosucceed de búsqueda:

    * objeto de usuario de Hello debe existir en hello espacio de conector de AD
    * objeto de usuario de Hello debe ser objeto de MV correspondiente toohello vinculado
    * objeto de usuario de Hello debe ser objeto de conector AAD correspondiente toohello vinculado.
    * Hello vínculo desde tooMV de objeto de conector AD debe tener reglas de sincronización de hello `Microsoft.InfromADUserAccountEnabled.xxx` en vínculo Hola. <br> <br>
    Cuando se recibe Hola llamada de nube de hello, usos de motor de sincronización de Hola Hola cloudAnchor toolook de atributo de objeto de espacio de conector AAD de Hola, sigue Hola vínculo toohello atrás MV objeto y, a continuación, sigue toohello atrás AD objeto de vínculo a Hola. Dado que podría haber varios objetos de Active Directory (varios bosques) para el mismo usuario, motor de sincronización de Hola se basa en Hola de Hola `Microsoft.InfromADUserAccountEnabled.xxx` Hola de vínculo toopick corregir uno.

    > [!Note]
    > Como resultado de esta lógica, Azure AD Connect debe ser capaz de toocommunicate con hello emulador de PDC para toowork de reescritura de contraseña. Si necesita tooenable este manualmente, puede conectarse toohello emulador de PDC de Azure AD Connect con el botón secundario en hello **propiedades** de conector de sincronización de Active Directory de hello, a continuación, seleccione **configurar particiones de directorio**. Desde allí, busque hello **configuración de conexión de controlador de dominio** y la sección de casilla Hola titulada **sólo utilizará los controladores de dominio preferidos**. Aunque Hola preferida que DC no es un emulador PDC, Azure AD Connect intentará tooconnect toohello PDC para la escritura diferida de contraseñas.

8. Una vez que se encuentra la cuenta de usuario de hello, intentamos contraseña de hello tooreset directamente en el bosque de AD de hello correspondiente.
9. Si se realiza correctamente la operación de establecimiento de contraseña de hello, indicamos a usuario Hola que se ha cambiado su contraseña.
    > [!NOTE]
    > En caso de Hola Hola contraseña una vez sincronizada tooAzure AD mediante la sincronización de contraseña, es probable que la directiva de contraseñas de local de hello es más débil que la directiva de contraseñas de hello en la nube. En este caso, se sigue aplicar cualquier directiva local de hello es y en su lugar permitir contraseña de hash de Hola de toosynchronize de sincronización de hash de contraseña. Esto garantiza que la directiva local se aplica en la nube de hello, sin importar si usa tooprovide de federación o sincronización de contraseña inicio de sesión único.

10. Si contraseña Hola establece operación provocará un error, se devuelve Hola error toohello al usuario y le permite intentarlo de nuevo.
    * la operación de Hello puede producir debido a la siguiente Hola
        * Hola servicio no estaba disponible
        * contraseña de Hello seleccionadas no cumple las directivas de la organización
        * No se pudo encontrar el usuario de Hola Hola AD local

    Tenemos un determinado mensaje para muchos de estos casos e informar al usuario de hello qué pueden hacer problema de hello tooresolve.

## <a name="configuring-password-writeback"></a>Configuración de la escritura diferida de contraseñas

Se recomienda usar la característica de actualización automática de Hola de [Azure AD Connect](./connect/active-directory-aadconnect-get-started-express.md) si desea que la escritura diferida de contraseñas de toouse.

DirSync y Azure AD Sync ya no son compatible medio de la habilitación de artículo de Hola de reescritura de contraseña [actualizar desde DirSync y Azure AD Sync](connect/active-directory-aadconnect-dirsync-deprecated.md) tiene más toohelp de información con la transición.

Hello siguiente da por sentado que ya ha configurado Azure AD Connect en su entorno mediante hello [Express](./connect/active-directory-aadconnect-get-started-express.md) o [personalizado](./connect/active-directory-aadconnect-get-started-custom.md) configuración.

1. escritura diferida de contraseñas tooconfigure y habilitar inicie sesión en tooyour AD Azure Connect server e inicie hello **Azure AD Connect** Asistente de configuración.
2. En la pantalla de bienvenida de bienvenida, haga clic en **configurar**.
3. En hello adicionales tareas pantalla haga clic en **personalizar las opciones de sincronización** y, a continuación, elija **siguiente**.
4. En la pantalla de bienvenida conectar tooAzure AD escriba una credencial de administrador Global y elija **siguiente**.
5. En hello, conectar los directorios y el dominio y unidad organizativa filtrado pantallas puede elegir **siguiente**.
6. En la pantalla de bienvenida características opcionales casilla Hola junto demasiado**escritura diferida de contraseñas** y haga clic en **siguiente**.
   ![Habilitar la escritura diferida de contraseñas en Azure AD Connect][Writeback]
7. En la pantalla de bienvenida tooconfigure listo, haga clic en **configurar** y espere Hola proceso toocomplete.
8. Cuando aparezca Configuración completa, puede hacer clic en **Salir**.

## <a name="licensing-requirements-for-password-writeback"></a>Requisitos de licencia para la escritura diferida de contraseñas

Para obtener información sobre licencia, vea tema hello [licencias necesitan para la escritura diferida de contraseñas](active-directory-passwords-licensing.md#licenses-required-for-password-writeback) u Hola después de sitios

* [Sitio sobre precios de Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/)
* [Enterprise Mobility + Security](https://www.microsoft.com/cloud-platform/enterprise-mobility-security)
* [Secure Productive Enterprise](https://www.microsoft.com/secure-productive-enterprise/default.aspx)

### <a name="on-premises-authentication-modes-supported-for-password-writeback"></a>Modos de autenticación local admitidos para la escritura diferida de contraseñas

Funciona de la escritura diferida de contraseñas para hello siguientes tipos de contraseña de usuario:

* **Usuarios solo en la nube**: La escritura diferida de contraseñas no se aplica en este caso, porque no hay contraseña local
* **Usuarios sincronizados con contraseña**: se admite la escritura diferida de contraseñas
* **Usuarios federados**: Se admite la escritura diferida de contraseñas
* **Usuarios de autenticación de paso a través**: Se admite la escritura diferida de contraseñas

### <a name="user-and-admin-operations-supported-for-password-writeback"></a>Operaciones de usuario y administrador admitidas para la escritura diferida de contraseñas

Las contraseñas se reescriben en hello todas las siguientes situaciones:

* **Operaciones de usuario final admitidas**
  * Cualquier operación de cambio de contraseña voluntaria de autoservicio del usuario final
  * Cualquier operación de cambio de contraseña exigida de autoservicio del usuario final (por ejemplo, la expiración de contraseña)
  * Cualquier contraseña de autoservicio para el usuario final restablece procedentes de hello [Portal de restablecimiento de contraseña](https://passwordreset.microsoftonline.com)
* **Operaciones de administrador admitidas**
  * Cualquier operación de cambio de contraseña voluntaria de autoservicio del administrador
  * Cualquier operación de cambio de contraseña exigida de autoservicio del administrador (por ejemplo, la expiración de contraseña)
  * Cualquier contraseña de autoservicio de administrador restablece procedentes de hello [Portal de restablecimiento de contraseña](https://passwordreset.microsoftonline.com)
  * Cualquier contraseña iniciadas por el administrador para el usuario final de restablecimiento de hello [portal de Azure clásico](https://manage.windowsazure.com)
  * Cualquier contraseña iniciadas por el administrador para el usuario final de restablecimiento de hello [portal de Azure](https://portal.azure.com)

### <a name="user-and-admin-operations-not-supported-for-password-writeback"></a>Operaciones de usuario y administrador no admitidas para la escritura diferida de contraseñas

Las contraseñas son **no** escrito en cualquiera de hello siguientes situaciones:

* **Operaciones de usuario final no admitidas**
  * Cualquier usuario restablecer su contraseña mediante PowerShell v1, v2 u Hola API de Azure AD Graph
* **Operaciones de administrador no admitidas**
  * Cualquier contraseña iniciadas por el administrador para el usuario final de restablecimiento de hello [portal de administración de Office](https://portal.office.com)
  * Cualquier contraseña iniciadas por el administrador para el usuario final restablecer desde PowerShell v1, v2 o hello Azure AD Graph API

Mientras estamos trabajando tooremove estas limitaciones, no tenemos una escala de tiempo concreto, que podemos compartir aún.

## <a name="password-writeback-security-model"></a>Modelo de seguridad de la escritura diferida de contraseñas

La escritura diferida de contraseñas es un servicio muy seguro.  tooensure que su información está protegida, habilitamos un modelo de 4 niveles de seguridad que se describe a continuación.

* **Service Bus Relay específico del inquilino**
  * Al configurar el servicio de hello, configuramos una retransmisión de bus de servicio específico del inquilino que está protegida por una contraseña segura generada aleatoriamente que Microsoft nunca tiene acceso.
* **Clave de cifrado de contraseñas bloqueadas y criptográficamente segura**
  * Una vez creada la retransmisión de bus de servicio de hello, crearemos una clave simétrica segura se use tooencrypt Hola contraseña llega por cable Hola. Esta clave reside solo en almacén secreto de su empresa en la nube de hello, que es muy bloqueada y auditar como cualquier contraseña en el directorio de Hola.
* **TLS estándar del sector**
  1. Al restablecer o cambiar una contraseña operación se produce en la nube de hello, tomamos la contraseña de texto simple de Hola y cifrar con la clave pública.
  2. A continuación, se coloque en un mensaje HTTPS, que se envía a través de un canal cifrado con la retransmisión de bus de servicio de tooyour certificados SSL de Microsoft.
  3. Después de mensaje de Hola llega al Bus de servicio, el agente local se reactiva la y autentica tooService Bus utilizando Hola contraseña segura que se generó anteriormente.
  4. Agente local recoge el mensaje cifrado hello, lo descifra utilizando la clave privada de hello generamos.
  5. Agente local, a continuación, intentos de contraseña de hello tooset a través de hello API SetPassword de AD DS.
     * Este paso es lo que nos permite tooenforce AD contraseña directiva local (complejidad, antigüedad, historial, filtros, etc.) en la nube de Hola.
* **Directivas de expiración de mensajes** 
  * Si el mensaje de bienvenida se ubica en el Bus de servicio porque el servicio local no está funcionando, agotará el tiempo de y se quitará después de varios minutos tooincrease aún más la seguridad.

### <a name="password-writeback-encryption-details"></a>Detalles de cifrado de la escritura diferida de contraseñas

a continuación se describen los pasos de cifrado de Hello atraviesa una solicitud de restablecimiento de contraseña después de que un usuario lo haya enviado, antes de que llegue en su entorno local, de tooensure servicio máxima confiabilidad y seguridad.

* **Paso 1: cifrado de contraseña con la clave de RSA de 2048 bits** : una vez que un usuario envía un toobe contraseña reescrito tooon local, en primer lugar, Hola enviado propia contraseña se cifra con una clave RSA de 2048 bits.
* **Paso 2: cifrado de nivel de paquete con AES-GCM** -, a continuación, el paquete completo de hello (contraseña + metadatos necesarios) se cifra mediante AES-GCM. Esto evita que cualquier persona con canal de bus de servicio de acceso directo toohello subyacente de visualización y manipulación con contenido de Hola.
* **Paso 3: toda la comunicación se produce a través de TLS / SSL** -todas las comunicaciones de hello con bus de servicio tiene lugar en un canal SSL/TLS. Esto protege contenido Hola de partes 3rd no autorizadas.
* **Sustitución de clave automática cada seis meses** : automáticamente cada 6 meses, o cada vez que escritura diferida de contraseñas está deshabilitado o volver a habilitar en Azure AD Connect, se sustitución todas estas claves de seguridad de servicio máximo de tooensure y seguridad.

### <a name="password-writeback-bandwidth-usage"></a>Uso de ancho de banda de la escritura diferida de contraseñas

Escritura diferida de contraseñas es un servicio de poco ancho de banda que envía solicitudes de realizar copias de agente de toohello local solo en hello siguientes circunstancias:

1. Dos de los mensajes enviados al habilitar o deshabilitar la característica de Hola a través de Azure AD Connect.
2. Se envía un mensaje una vez cada cinco minutos como un latido de servicio para siempre y cuando el servicio de saludo se está ejecutando.
3. Se envían dos mensajes cada vez que se envía una nueva contraseña.
    * Primer mensaje, como una operación de solicitud tooperform Hola
    * Segundo mensaje, que contiene el resultado de hello de operación de Hola y se envía en hello siguientes circunstancias:
        * Cada vez que se envía una nueva contraseña durante un restablecimiento de la contraseña de autoservicio de un usuario.
        * Cada vez que se envía una nueva contraseña durante una operación de cambio de la contraseña de un usuario.
        * Cada vez que se envía una nueva contraseña durante una contraseña de usuario iniciadas por el administrador restablecer (a través de los portales solo de hello administración de Azure).

#### <a name="message-size-and-bandwidth-considerations"></a>Consideraciones sobre el ancho de banda y el tamaño de mensaje

Hola tamaño de cada uno de los mensajes de Hola que se ha descrito anteriormente suele ser menos de 1 kb, incluso bajo cargas extremas, servicio de escritura diferida de contraseña de hello propio está consumiendo unos kilobits por segundo del ancho de banda. Puesto que cada mensaje se envía en tiempo real, sólo cuando sea necesario por una operación de actualización de contraseña y, puesto que el tamaño del mensaje de Hola es tan pequeño, uso de ancho de banda de Hola de capacidad de reescritura de hello eficazmente es demasiado pequeño toohave cualquier impacto cuantificable real.

## <a name="next-steps"></a>Pasos siguientes

Hola siguientes vínculos proporciona más información sobre el uso de Azure AD de restablecimiento de contraseña

* [**Inicio rápido**](active-directory-passwords-getting-started.md): preparativos para el autoservicio de administración de contraseñas de Azure AD 
* [**Licencias**](active-directory-passwords-licensing.md): configuración de licencias de Azure AD
* [**Datos** ](active-directory-passwords-data.md) : comprender los datos de Hola que es necesarios y cómo se utiliza para la administración de contraseñas
* [**Implementación** ](active-directory-passwords-best-practices.md) -planear e implementar a los usuarios de Autoservicio tooyour usando la orientación de hello encontrar aquí
* [**Personalizar** ](active-directory-passwords-customize.md) -personalizar Hola apariencia y funcionamiento del programa Hola a la experiencia de Autoservicio de su empresa.
* [**Directiva**](active-directory-passwords-policy.md): información sobre las directivas de contraseñas de Azure AD y cómo establecerlas
* [**Informes**](active-directory-passwords-reporting.md): detectan si los usuarios acceden a la funcionalidad de SSPR, cuándo lo hacen y dónde.
* [**Profundización técnica** ](active-directory-passwords-how-it-works.md) -ir detrás de hello cortina toounderstand cómo funciona
* [**Preguntas más frecuentes**](active-directory-passwords-faq.md): ¿Cómo? ¿Por qué? ¿Qué? ¿Dónde? ¿Quién? ¿Cuándo? -Responde tooquestions siempre deseara tooask
* [**Solucionar problemas de** ](active-directory-passwords-troubleshoot.md) -Obtenga información acerca de cómo problemas comunes de tooresolve que vemos con SSPR

[Writeback]: ./media/active-directory-passwords-writeback/enablepasswordwriteback.png "Habilitar la escritura diferida de contraseñas en Azure AD Connect"
