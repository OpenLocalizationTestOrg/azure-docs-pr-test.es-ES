---
title: "aaaSilent instalar el conector del Proxy de aplicación de Azure AD | Documentos de Microsoft"
description: "Explica cómo tooperform una instalación desatendida de conector del Proxy de aplicación de Azure AD tooprovide el acceso remoto seguro tooyour local las aplicaciones."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 3aa1c7f2-fb2a-4693-abd5-95bb53700cbb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: ce796ff45a65ba7d5f0f63c02085bdc6af494548
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="silently-install-hello-azure-ad-application-proxy-connector"></a>Realizar una instalación silenciosa Hola conector del Proxy de aplicación de Azure AD
Desea toobe toosend capaz de una instalación de script toomultiple Windows servidores o tooWindows servidores que no tienen interfaz de usuario habilitado. Este tema le ayuda a crear un script de Windows PowerShell que hace posible la instalación desatendida y el registro para el conector del proxy de la aplicación de Azure AD.

Esta capacidad resulta útil cuando desea hacer lo siguiente:

* Instale el conector de hello en máquinas con ninguna capa de interfaz de usuario o cuando no se puede máquina toohello RDP.
* Instalar y registrar muchos conectores a la vez.
* Integrar la instalación del conector de Hola y el registro como parte de otro procedimiento.
* Crear una imagen de servidor estándar que contiene Hola conector bits pero no está registrada.

Proxy de aplicación funciona mediante la instalación de un servicio de Windows Server fino llamado hello conector dentro de la red. Para toowork de conector del Proxy de aplicación hello tiene toobe registrado con su directorio de Azure AD mediante un administrador global y una contraseña. Normalmente esta información se especifica durante la instalación del conector en un cuadro de diálogo emergente. Sin embargo, puede usar la información de registro toocreate un tooenter de objeto de credencial de Windows PowerShell. O puede crear su propio token y usarlo tooenter la información de registro.

## <a name="install-hello-connector"></a>Instalar el conector de Hola
Instalar msi del conector Hola sin registrar Hola conector como sigue:

1. Abra el símbolo del sistema.
2. Ejecute el siguiente comando en qué Hola/q implica la instalación silenciosa de hello: hello instalación no solicita tooaccept Hola contrato de licencia para el usuario final.
   
        AADApplicationProxyConnectorInstaller.exe REGISTERCONNECTOR="false" /q

## <a name="register-hello-connector-with-azure-ad"></a>Registrar el conector de hello con Azure AD
Hay dos métodos que puede utilizar el conector de Hola tooregister:

* Registrar el conector de hello mediante un objeto de credencial de Windows PowerShell
* Registrar el conector Hola utilizando un token creado sin conexión

### <a name="register-hello-connector-using-a-windows-powershell-credential-object"></a>Registrar el conector de hello mediante un objeto de credencial de Windows PowerShell
1. Crear objeto de credenciales de Windows PowerShell de hello, ejecute este comando. Reemplace  *\<nombre de usuario\>*  y  *\<contraseña\>*  con hello username y password para su directorio:
   
        $User = "<username>"
        $PlainPassword = '<password>'
        $SecurePassword = $PlainPassword | ConvertTo-SecureString -AsPlainText -Force
        $cred = New-Object –TypeName System.Management.Automation.PSCredential –ArgumentList $User, $SecurePassword
2. Vaya demasiado**conector del Proxy de aplicación de C:\Program Files\Microsoft AAD** y ejecutar script de Hola con hello PowerShell credenciales de objeto creado. Reemplace *$cred* con nombre Hola de hello PowerShell credenciales objeto creado:
   
        RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Credentials -Usercredentials $cred

### <a name="register-hello-connector-using-a-token-created-offline"></a>Registrar el conector Hola utilizando un token creado sin conexión
1. Crear un símbolo (token) sin conexión mediante hello AuthenticationContext clase usa valores de hello en el fragmento de código de hello:

        using System;
        using System.Diagnostics;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;

        class Program
        {
        #region constants
        /// <summary>
        /// hello AAD authentication endpoint uri
        /// </summary>
        static readonly Uri AadAuthenticationEndpoint = new Uri("https://login.microsoftonline.com/common/oauth2/token?api-version=1.0");

        /// <summary>
        /// hello application ID of hello connector in AAD
        /// </summary>
        static readonly string ConnectorAppId = "55747057-9b5d-4bd4-b387-abf52a8bd489";

        /// <summary>
        /// hello reply address of hello connector application in AAD
        /// </summary>
        static readonly Uri ConnectorRedirectAddress = new Uri("urn:ietf:wg:oauth:2.0:oob");

        /// <summary>
        /// hello AppIdUri of hello registration service in AAD
        /// </summary>
        static readonly Uri RegistrationServiceAppIdUri = new Uri("https://proxy.cloudwebappproxy.net/registerapp");

        #endregion

        #region private members
        private string token;
        private string tenantID;
        #endregion

        public void GetAuthenticationToken()
        {
            AuthenticationContext authContext = new AuthenticationContext(AadAuthenticationEndpoint.AbsoluteUri);

            AuthenticationResult authResult = authContext.AcquireToken(RegistrationServiceAppIdUri.AbsoluteUri,
                ConnectorAppId,
                ConnectorRedirectAddress,
                PromptBehavior.Always);

            if (authResult == null || string.IsNullOrEmpty(authResult.AccessToken) || string.IsNullOrEmpty(authResult.TenantId))
            {
                Trace.TraceError("Authentication result, token or tenant id returned are null");
                throw new InvalidOperationException("Authentication result, token or tenant id returned are null");
            }

            token = authResult.AccessToken;
            tenantID = authResult.TenantId;
        }


2. Una vez que tenga el token de hello, cree una cadena segura mediante el símbolo (token) de hello:

   `$SecureToken = $Token | ConvertTo-SecureString -AsPlainText -Force`

3. Hola ejecución siguiente comando de Windows PowerShell, reemplazar \<inquilino GUID\> con su Id. de directorio:

   `RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Token -Token $SecureToken -TenantId <tenant GUID>`

## <a name="next-steps"></a>Pasos siguientes 
* [Publicar aplicaciones mediante su propio nombre de dominio](active-directory-application-proxy-custom-domains.md)
* [Habilitar el inicio de sesión único](active-directory-application-proxy-sso-using-kcd.md)
* [Solucionar los problemas que tiene con el Proxy de aplicación](active-directory-application-proxy-troubleshoot.md)


