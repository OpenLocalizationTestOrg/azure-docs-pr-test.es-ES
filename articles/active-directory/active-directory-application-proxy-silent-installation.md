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
# <a name="silently-install-hello-azure-ad-application-proxy-connector"></a><span data-ttu-id="23fc3-103">Realizar una instalación silenciosa Hola conector del Proxy de aplicación de Azure AD</span><span class="sxs-lookup"><span data-stu-id="23fc3-103">Silently install hello Azure AD Application Proxy Connector</span></span>
<span data-ttu-id="23fc3-104">Desea toobe toosend capaz de una instalación de script toomultiple Windows servidores o tooWindows servidores que no tienen interfaz de usuario habilitado.</span><span class="sxs-lookup"><span data-stu-id="23fc3-104">You want toobe able toosend an installation script toomultiple Windows servers or tooWindows Servers that don't have user interface enabled.</span></span> <span data-ttu-id="23fc3-105">Este tema le ayuda a crear un script de Windows PowerShell que hace posible la instalación desatendida y el registro para el conector del proxy de la aplicación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="23fc3-105">This topic helps you create a Windows PowerShell script that enables unattended installation and registration for your Azure AD Application Proxy Connector.</span></span>

<span data-ttu-id="23fc3-106">Esta capacidad resulta útil cuando desea hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="23fc3-106">This capability is useful when you want to:</span></span>

* <span data-ttu-id="23fc3-107">Instale el conector de hello en máquinas con ninguna capa de interfaz de usuario o cuando no se puede máquina toohello RDP.</span><span class="sxs-lookup"><span data-stu-id="23fc3-107">Install hello connector on machines with no UI layer or when you cannot RDP toohello machine.</span></span>
* <span data-ttu-id="23fc3-108">Instalar y registrar muchos conectores a la vez.</span><span class="sxs-lookup"><span data-stu-id="23fc3-108">Install and register many connectors at once.</span></span>
* <span data-ttu-id="23fc3-109">Integrar la instalación del conector de Hola y el registro como parte de otro procedimiento.</span><span class="sxs-lookup"><span data-stu-id="23fc3-109">Integrate hello connector installation and registration as part of another procedure.</span></span>
* <span data-ttu-id="23fc3-110">Crear una imagen de servidor estándar que contiene Hola conector bits pero no está registrada.</span><span class="sxs-lookup"><span data-stu-id="23fc3-110">Create a standard server image that contains hello connector bits but is not registered.</span></span>

<span data-ttu-id="23fc3-111">Proxy de aplicación funciona mediante la instalación de un servicio de Windows Server fino llamado hello conector dentro de la red.</span><span class="sxs-lookup"><span data-stu-id="23fc3-111">Application Proxy works by installing a slim Windows Server service called hello Connector inside your network.</span></span> <span data-ttu-id="23fc3-112">Para toowork de conector del Proxy de aplicación hello tiene toobe registrado con su directorio de Azure AD mediante un administrador global y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="23fc3-112">For hello Application Proxy Connector toowork it has toobe registered with your Azure AD directory using a global administrator and password.</span></span> <span data-ttu-id="23fc3-113">Normalmente esta información se especifica durante la instalación del conector en un cuadro de diálogo emergente.</span><span class="sxs-lookup"><span data-stu-id="23fc3-113">Ordinarily this information is entered during Connector installation in a pop-up dialog box.</span></span> <span data-ttu-id="23fc3-114">Sin embargo, puede usar la información de registro toocreate un tooenter de objeto de credencial de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="23fc3-114">However, you can use Windows PowerShell toocreate a credential object tooenter your registration information.</span></span> <span data-ttu-id="23fc3-115">O puede crear su propio token y usarlo tooenter la información de registro.</span><span class="sxs-lookup"><span data-stu-id="23fc3-115">Or you can create your own token and use it tooenter your registration information.</span></span>

## <a name="install-hello-connector"></a><span data-ttu-id="23fc3-116">Instalar el conector de Hola</span><span class="sxs-lookup"><span data-stu-id="23fc3-116">Install hello connector</span></span>
<span data-ttu-id="23fc3-117">Instalar msi del conector Hola sin registrar Hola conector como sigue:</span><span class="sxs-lookup"><span data-stu-id="23fc3-117">Install hello Connector MSIs without registering hello Connector as follows:</span></span>

1. <span data-ttu-id="23fc3-118">Abra el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="23fc3-118">Open a command prompt.</span></span>
2. <span data-ttu-id="23fc3-119">Ejecute el siguiente comando en qué Hola/q implica la instalación silenciosa de hello: hello instalación no solicita tooaccept Hola contrato de licencia para el usuario final.</span><span class="sxs-lookup"><span data-stu-id="23fc3-119">Run hello following command in which hello /q means quiet installation - hello installation doesn't prompt you tooaccept hello End-User License Agreement.</span></span>
   
        AADApplicationProxyConnectorInstaller.exe REGISTERCONNECTOR="false" /q

## <a name="register-hello-connector-with-azure-ad"></a><span data-ttu-id="23fc3-120">Registrar el conector de hello con Azure AD</span><span class="sxs-lookup"><span data-stu-id="23fc3-120">Register hello connector with Azure AD</span></span>
<span data-ttu-id="23fc3-121">Hay dos métodos que puede utilizar el conector de Hola tooregister:</span><span class="sxs-lookup"><span data-stu-id="23fc3-121">There are two methods you can use tooregister hello connector:</span></span>

* <span data-ttu-id="23fc3-122">Registrar el conector de hello mediante un objeto de credencial de Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="23fc3-122">Register hello connector using a Windows PowerShell credential object</span></span>
* <span data-ttu-id="23fc3-123">Registrar el conector Hola utilizando un token creado sin conexión</span><span class="sxs-lookup"><span data-stu-id="23fc3-123">Register hello connector using a token created offline</span></span>

### <a name="register-hello-connector-using-a-windows-powershell-credential-object"></a><span data-ttu-id="23fc3-124">Registrar el conector de hello mediante un objeto de credencial de Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="23fc3-124">Register hello connector using a Windows PowerShell credential object</span></span>
1. <span data-ttu-id="23fc3-125">Crear objeto de credenciales de Windows PowerShell de hello, ejecute este comando.</span><span class="sxs-lookup"><span data-stu-id="23fc3-125">Create hello Windows PowerShell Credentials object by running this command.</span></span> <span data-ttu-id="23fc3-126">Reemplace  *\<nombre de usuario\>*  y  *\<contraseña\>*  con hello username y password para su directorio:</span><span class="sxs-lookup"><span data-stu-id="23fc3-126">Replace *\<username\>* and *\<password\>* with hello username and password for your directory:</span></span>
   
        $User = "<username>"
        $PlainPassword = '<password>'
        $SecurePassword = $PlainPassword | ConvertTo-SecureString -AsPlainText -Force
        $cred = New-Object –TypeName System.Management.Automation.PSCredential –ArgumentList $User, $SecurePassword
2. <span data-ttu-id="23fc3-127">Vaya demasiado**conector del Proxy de aplicación de C:\Program Files\Microsoft AAD** y ejecutar script de Hola con hello PowerShell credenciales de objeto creado.</span><span class="sxs-lookup"><span data-stu-id="23fc3-127">Go too**C:\Program Files\Microsoft AAD App Proxy Connector** and run hello script using hello PowerShell credentials object you created.</span></span> <span data-ttu-id="23fc3-128">Reemplace *$cred* con nombre Hola de hello PowerShell credenciales objeto creado:</span><span class="sxs-lookup"><span data-stu-id="23fc3-128">Replace *$cred* with hello name of hello PowerShell credentials object you created:</span></span>
   
        RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Credentials -Usercredentials $cred

### <a name="register-hello-connector-using-a-token-created-offline"></a><span data-ttu-id="23fc3-129">Registrar el conector Hola utilizando un token creado sin conexión</span><span class="sxs-lookup"><span data-stu-id="23fc3-129">Register hello connector using a token created offline</span></span>
1. <span data-ttu-id="23fc3-130">Crear un símbolo (token) sin conexión mediante hello AuthenticationContext clase usa valores de hello en el fragmento de código de hello:</span><span class="sxs-lookup"><span data-stu-id="23fc3-130">Create an offline token using hello AuthenticationContext class using hello values in hello code snippet:</span></span>

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


2. <span data-ttu-id="23fc3-131">Una vez que tenga el token de hello, cree una cadena segura mediante el símbolo (token) de hello:</span><span class="sxs-lookup"><span data-stu-id="23fc3-131">Once you have hello token, create a SecureString using hello token:</span></span>

   `$SecureToken = $Token | ConvertTo-SecureString -AsPlainText -Force`

3. <span data-ttu-id="23fc3-132">Hola ejecución siguiente comando de Windows PowerShell, reemplazar \<inquilino GUID\> con su Id. de directorio:</span><span class="sxs-lookup"><span data-stu-id="23fc3-132">Run hello following Windows PowerShell command, replacing \<tenant GUID\> with your directory ID:</span></span>

   `RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Token -Token $SecureToken -TenantId <tenant GUID>`

## <a name="next-steps"></a><span data-ttu-id="23fc3-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="23fc3-133">Next steps</span></span> 
* [<span data-ttu-id="23fc3-134">Publicar aplicaciones mediante su propio nombre de dominio</span><span class="sxs-lookup"><span data-stu-id="23fc3-134">Publish applications using your own domain name</span></span>](active-directory-application-proxy-custom-domains.md)
* [<span data-ttu-id="23fc3-135">Habilitar el inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="23fc3-135">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
* [<span data-ttu-id="23fc3-136">Solucionar los problemas que tiene con el Proxy de aplicación</span><span class="sxs-lookup"><span data-stu-id="23fc3-136">Troubleshoot issues you're having with Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)


