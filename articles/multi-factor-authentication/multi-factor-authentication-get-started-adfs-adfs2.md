---
title: Servidor de Azure MFA con AD FS 2.0 aaaUse | Documentos de Microsoft
description: "Se trata de una página de autenticación multifactor de Azure de Hola que describe cómo se inicia tooget con MFA de Azure y AD FS 2.0."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 96168849-241a-4499-a224-d829913caa7e
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/14/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: H1Hack27Feb2017, it-pro
ms.openlocfilehash: 15011a94ca69dc6e51aa3edf74f5db6cd44d697a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-multi-factor-authentication-server-toowork-with-ad-fs-20"></a>Configurar el servidor de autenticación multifactor de Azure toowork con AD FS 2.0
Este artículo es para las organizaciones que se federan con Azure Active Directory y desea recursos toosecure en local o en la nube de Hola. Proteger los recursos utilizando Hola servidor Azure Multi-factor Authentication y configurándolo toowork con AD FS para que la verificación en dos pasos se desencadene para extremos de gran valor.

Esta documentación incluye el uso de hello servidor Azure Multi-factor Authentication con AD FS 2.0. Para información sobre AD FS, consulte [Protección de recursos en la nube y locales mediante Servidor Azure Multi-Factor Authentication con Windows Server 2012 R2 AD FS](multi-factor-authentication-get-started-adfs-w2k12.md).

## <a name="secure-ad-fs-20-with-a-proxy"></a>Protección de AD FS 2.0 con un proxy
toosecure AD FS 2.0 con un proxy, instale Hola servidor Azure Multi-factor Authentication en el servidor de proxy de hello AD FS.

### <a name="configure-iis-authentication"></a>Configuración de la autenticación de IIS
1. Hola servidor Azure Multi-factor Authentication, haga clic en hello **autenticación IIS** icono en el menú de la izquierda Hola.
2. Haga clic en hello **basada en formularios** ficha.
3. Haga clic en **Agregar**.

   <center>![Configuración](./media/multi-factor-authentication-get-started-adfs-adfs2/setup1.png)</center>

4. variables de nombre de usuario, contraseña y dominio toodetect automáticamente, escriba la dirección URL de inicio de sesión de hello (por ejemplo, https://sso.contoso.com/adfs/ls) en el cuadro de diálogo de hello automática de sitio Web y haga clic en **Aceptar**.
5. Comprobar hello **coincidencia de usuario requieren la autenticación multifactor Azure** cuadro si todos los usuarios se han o se importarán en hello Server y la comprobación de paso tootwo de asunto. Si un número significativo de usuarios no se ha importado en hello servidor y/o se va a excluir de la verificación en dos pasos, deje el cuadro de hello desactivada.
6. Si no se detectan automáticamente las variables de página de hello, haga clic en hello **especificar manualmente...** botón en el cuadro de diálogo de hello automática de sitio Web.
7. En el cuadro de diálogo Agregar sitio Web de hello, especifique la página de inicio de sesión de hello URL toohello AD FS en el campo de dirección URL de envío de hello (por ejemplo, https://sso.contoso.com/adfs/ls) y escriba un nombre de la aplicación (opcional). nombre de la aplicación Hello aparece en los informes de la autenticación multifactor Azure y puede mostrarse en mensajes de autenticación SMS o aplicación móvil.
8. Establecer el formato de solicitud de hello demasiado**POST o GET**.
9. Escriba la variable de nombre de usuario de hello (ctl00$ ContentPlaceHolder1$ UsernameTextBox) y la variable de contraseña (ctl00$ ContentPlaceHolder1$ PasswordTextBox). Si la página de inicio de sesión basado en formularios muestra un cuadro de texto dominio, escriba la variable de dominio de Hola. nombres de hello toofind de cuadros de entrada de hello en la página de inicio de sesión de hello, página de inicio de sesión de toohello vaya en un explorador web, haga doble clic en página de Hola y seleccione **ver código fuente**.
10. Comprobar hello **coincidencia de usuario requieren la autenticación multifactor Azure** cuadro si todos los usuarios se han o se importarán en hello Server y la comprobación de paso tootwo de asunto. Si un número significativo de usuarios no se ha importado en hello servidor y/o se va a excluir de la verificación en dos pasos, deje el cuadro de hello desactivada.
    <center>![Configuración](./media/multi-factor-authentication-get-started-adfs-adfs2/manual.png)</center>
11. Haga clic en **Avanzadas…** tooreview configuración avanzada. Entre los valores que puede configurar, se incluyen:

    - Seleccionar un archivo de página de denegación personalizado
    - Uso de cookies sitio Web de toohello de las autenticaciones correctas de caché
    - Seleccione cómo tooauthenticate Hola credenciales principales

12. Puesto que no es probable que el servidor proxy de hello AD FS toobe Unidos a un dominio de toohello, puede usar el controlador de dominio de tooyour tooconnect LDAP para la autenticación previa y la importación de usuarios. En el cuadro de diálogo del sitio Web basado de hello, haga clic en hello **autenticación principal** pestaña y seleccione **enlace LDAP** para el tipo de autenticación de la autenticación previa de Hola.
13. Cuando haya terminado, haga clic en **Aceptar** cuadro de diálogo Agregar sitio Web de tooreturn toohello.
14. Haga clic en **Aceptar** cuadro de diálogo de tooclose Hola.
15. Una vez Hola dirección URL y las variables de página se han detectado o especificado, datos del sitio Web de hello muestran de Hola panel basado en formularios.
16. Haga clic en hello **módulo nativo** pestaña y seleccione Hola servidor, sitio Web de hello proxy de hello AD FS se ejecuta bajo (como "sitio Web predeterminado"), u Hola Hola de tooenable aplicación (por ejemplo, "ls" en "adfs") de AD FS proxy complemento en Hola de IIS nivel deseado.
17. Haga clic en hello **autenticación habilitar IIS** cuadro situado en la parte superior de Hola de pantalla de bienvenida.

autenticación de IIS de Hello está habilitada.

### <a name="configure-directory-integration"></a>Configuración de la integración de directorios
Ha habilitado la autenticación de IIS, pero tooperform Hola autenticación previa tooyour Active Directory (AD) mediante LDAP, debe configurar Hola controlador de dominio de toohello de conexión de LDAP.

1. Haga clic en hello **integración de directorios** icono.
2. En la pestaña de configuración de hello, seleccione hello **utilizar la configuración LDAP específica** botón de radio.

   <center>![Configuración](./media/multi-factor-authentication-get-started-adfs-adfs2/ldap1.png)</center>

3. Haga clic en **Editar**.
4. En el cuadro de diálogo Editar configuración de LDAP de hello, rellenar los campos de hello con controlador de dominio de hello información tooconnect requiere toohello AD. Se incluyen descripciones de campos de hello en el archivo de Ayuda del servidor de autenticación multifactor de Azure de Hola.
5. Probar conexión de LDAP de hello haciendo clic en hello **prueba** botón.

   <center>![Configuración](./media/multi-factor-authentication-get-started-adfs-adfs2/ldap2.png)</center>

6. Si la prueba de conexión de LDAP de hello fue correcta, haga clic en **Aceptar**.

### <a name="configure-company-settings"></a>Configuración de compañía
1. A continuación, haga clic en hello **configuración de la empresa** icono y seleccione hello **resolución de nombre de usuario** ficha.
2. Seleccione hello **atributo del identificador único usar LDAP para la coincidencia de nombres de usuario** botón de radio.
3. Si los usuarios escribir su nombre de usuario en formato "dominio ombre de usuario", Hola Server necesita toobe dominio de hello toostrip puede desactivar el nombre de usuario de hello cuando crea consultas LDAP de Hola. Esto puede hacerse mediante un valor del Registro.
4. Abra el editor del registro de hello y vaya tooHKEY_LOCAL_MACHINE/SOFTWARE/Wow6432Node/Positive redes/PhoneFactor en un servidor de 64 bits. Si se encuentra en un servidor de 32 bits, tomar Hola "Wow6432Node" fuera de la ruta de acceso de Hola. Cree un valor DWORD clave del registro denominada "UsernameCxz_stripPrefixDomain" y establezca Hola valor too1. La autenticación multifactor Azure ahora es la protección de proxy de AD FS Hola.

Asegúrese de que los usuarios se han importado desde Active Directory en hello Server. Vea hello [sección de IP de confianza](#trusted-ips) si le gustaría toowhitelist direcciones IP internas para que no se requiera la verificación en dos pasos cuando inicien sesión en el sitio Web de toohello desde estas ubicaciones.

<center>![Configuración](./media/multi-factor-authentication-get-started-adfs-adfs2/reg.png)</center>

## <a name="ad-fs-20-direct-without-a-proxy"></a>AD FS 2.0 Direct sin proxy
Puede proteger ADFS cuando no se utiliza el proxy de hello AD FS. Instale Hola servidor Azure Multi-factor Authentication en el servidor de AD FS de Hola y configure Hola servidor por hello siguiendo los pasos:

1. Dentro de hello servidor Azure Multi-factor Authentication, haga clic en hello **autenticación IIS** icono en el menú de la izquierda Hola.
2. Haga clic en hello **HTTP** ficha.
3. Haga clic en **Agregar**.
4. En el cuadro de diálogo Agregar URL Base de hello, escriba Hola URL para el sitio Web de AD FS donde se realiza la autenticación HTTP (por ejemplo, https://sso.domain.com/adfs/ls/auth/integrated) en el campo de dirección URL Base Hola Hola. A continuación, escriba un nombre de la aplicación (opcional). nombre de la aplicación Hello aparece en los informes de la autenticación multifactor Azure y puede mostrarse en mensajes de autenticación SMS o aplicación móvil.
5. Si lo desea, ajustar el tiempo de espera de inactividad de Hola y el máximo tiempo de sesión.
6. Comprobar hello **coincidencia de usuario requieren la autenticación multifactor Azure** cuadro si todos los usuarios se han o se importarán en hello Server y la comprobación de paso tootwo de asunto. Si un número significativo de usuarios no se ha importado en hello servidor y/o se va a excluir de la verificación en dos pasos, deje el cuadro de hello desactivada.
7. Active la casilla de caché de cookies de hello si lo desea.

   <center>![Configuración](./media/multi-factor-authentication-get-started-adfs-adfs2/noproxy.png)</center>

8. Haga clic en **Aceptar**.
9. Haga clic en hello **módulo nativo** nivel deseado de pestaña y seleccione Hola servidor, Hola sitio Web (como "sitio Web predeterminado") u Hola AD FS aplicación (por ejemplo, "ls" en "adfs") tooenable Hola complemento en Hola de IIS.
10. Haga clic en hello **autenticación habilitar IIS** cuadro situado en la parte superior de Hola de pantalla de bienvenida.

Azure Multi-Factor Authentication protege ahora AD FS.

Asegúrese de que los usuarios se han importado desde Active Directory en hello Server. Consulte la sección de direcciones IP de confianza si desea que la dirección IP interna de toowhitelist Hola direcciones para que no se requiera la verificación en dos pasos cuando inicien sesión en el sitio Web de toohello desde estas ubicaciones.

## <a name="trusted-ips"></a>IP de confianza
IP de confianza permiten a los usuarios toobypass Azure la autenticación multifactor para solicitudes de sitios Web que se originan de direcciones IP o subredes específico. Por ejemplo, puede que desee tooexempt a los usuarios de verificación en dos pasos cuando inician sesión en desde office Hola. Para ello, especificaría la subred de la oficina de hello como una entrada de IP de confianza.

### <a name="tooconfigure-trusted-ips"></a>tooconfigure IP de confianza
1. Hola sección de autenticación de IIS, haga clic en hello **IP de confianza** ficha.
2. Haga clic en hello **agregar...** .
3. Cuando aparezca el cuadro de diálogo Agregar IP de confianza de hello, seleccione uno de hello **IP única**, **intervalo de IP**, o **subred** botones de radio.
4. Escriba la dirección IP de hello, intervalo de direcciones IP o subred que debe estar en la lista blanca. Si introduces una subred, seleccione Hola Hola adecuado de máscara de red y haga clic en **Aceptar** botón. Hola confianza que IP se ha agregado.

<center>![Configuración](./media/multi-factor-authentication-get-started-adfs-adfs2/trusted.png)</center>
