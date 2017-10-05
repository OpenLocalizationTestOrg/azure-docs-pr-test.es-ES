---
title: "Instalación silenciosa del conector del proxy de la aplicación de Azure AD | Microsoft Docs"
description: "Explica cómo realizar una instalación no atendida del conector de Proxy de aplicación de Azure AD para proporcionar acceso remoto seguro a las aplicaciones locales."
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
ms.openlocfilehash: 9e28c89d8f64f0ae3d4150017ca544e606075c45
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="silently-install-the-azure-ad-application-proxy-connector"></a><span data-ttu-id="e8c48-103">Instalación silenciosa del conector del proxy de la aplicación de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e8c48-103">Silently install the Azure AD Application Proxy Connector</span></span>
<span data-ttu-id="e8c48-104">Quiere poder enviar un script de instalación a varios servidores de Windows o servidores de Windows Server que no tienen habilitada la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="e8c48-104">You want to be able to send an installation script to multiple Windows servers or to Windows Servers that don't have user interface enabled.</span></span> <span data-ttu-id="e8c48-105">Este tema le ayuda a crear un script de Windows PowerShell que hace posible la instalación desatendida y el registro para el conector del proxy de la aplicación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e8c48-105">This topic helps you create a Windows PowerShell script that enables unattended installation and registration for your Azure AD Application Proxy Connector.</span></span>

<span data-ttu-id="e8c48-106">Esta capacidad resulta útil cuando desea hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="e8c48-106">This capability is useful when you want to:</span></span>

* <span data-ttu-id="e8c48-107">Instalar el conector en máquinas sin ninguna capa de interfaz de usuario o cuando no puede usar RDP en la máquina.</span><span class="sxs-lookup"><span data-stu-id="e8c48-107">Install the connector on machines with no UI layer or when you cannot RDP to the machine.</span></span>
* <span data-ttu-id="e8c48-108">Instalar y registrar muchos conectores a la vez.</span><span class="sxs-lookup"><span data-stu-id="e8c48-108">Install and register many connectors at once.</span></span>
* <span data-ttu-id="e8c48-109">Integrar la instalación del conector y el registro como parte de otro procedimiento.</span><span class="sxs-lookup"><span data-stu-id="e8c48-109">Integrate the connector installation and registration as part of another procedure.</span></span>
* <span data-ttu-id="e8c48-110">Crear una imagen de servidor estándar que contiene los bits de conector, pero no está registrada.</span><span class="sxs-lookup"><span data-stu-id="e8c48-110">Create a standard server image that contains the connector bits but is not registered.</span></span>

<span data-ttu-id="e8c48-111">El proxy de la aplicación funciona mediante la instalación de un pequeño servicio de Windows Server denominado conector dentro de la red.</span><span class="sxs-lookup"><span data-stu-id="e8c48-111">Application Proxy works by installing a slim Windows Server service called the Connector inside your network.</span></span> <span data-ttu-id="e8c48-112">Para que el conector de Proxy de aplicación funcione debe estar registrado con el directorio de Azure AD mediante un administrador global y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="e8c48-112">For the Application Proxy Connector to work it has to be registered with your Azure AD directory using a global administrator and password.</span></span> <span data-ttu-id="e8c48-113">Normalmente esta información se especifica durante la instalación del conector en un cuadro de diálogo emergente.</span><span class="sxs-lookup"><span data-stu-id="e8c48-113">Ordinarily this information is entered during Connector installation in a pop-up dialog box.</span></span> <span data-ttu-id="e8c48-114">Sin embargo, puede usar Windows PowerShell para crear un objeto de credencial a fin de especificar la información de registro.</span><span class="sxs-lookup"><span data-stu-id="e8c48-114">However, you can use Windows PowerShell to create a credential object to enter your registration information.</span></span> <span data-ttu-id="e8c48-115">O bien, puede crear su propio token y usarlo para escribir la información de registro.</span><span class="sxs-lookup"><span data-stu-id="e8c48-115">Or you can create your own token and use it to enter your registration information.</span></span>

## <a name="install-the-connector"></a><span data-ttu-id="e8c48-116">Instalación del conector</span><span class="sxs-lookup"><span data-stu-id="e8c48-116">Install the connector</span></span>
<span data-ttu-id="e8c48-117">Instale los MSI del conector sin registrar el conector de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="e8c48-117">Install the Connector MSIs without registering the Connector as follows:</span></span>

1. <span data-ttu-id="e8c48-118">Abra el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="e8c48-118">Open a command prompt.</span></span>
2. <span data-ttu-id="e8c48-119">Ejecute el siguiente comando en el que el modificador /q significa instalación desatendida (la instalación no le pide que acepte el contrato de licencia de usuario final).</span><span class="sxs-lookup"><span data-stu-id="e8c48-119">Run the following command in which the /q means quiet installation - the installation doesn't prompt you to accept the End-User License Agreement.</span></span>
   
        AADApplicationProxyConnectorInstaller.exe REGISTERCONNECTOR="false" /q

## <a name="register-the-connector-with-azure-ad"></a><span data-ttu-id="e8c48-120">Registro del conector con Azure AD</span><span class="sxs-lookup"><span data-stu-id="e8c48-120">Register the connector with Azure AD</span></span>
<span data-ttu-id="e8c48-121">Hay dos métodos posibles para registrar el conector:</span><span class="sxs-lookup"><span data-stu-id="e8c48-121">There are two methods you can use to register the connector:</span></span>

* <span data-ttu-id="e8c48-122">Registro del conector mediante un objeto de credenciales de Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="e8c48-122">Register the connector using a Windows PowerShell credential object</span></span>
* <span data-ttu-id="e8c48-123">Registro del conector mediante un token creado sin conexión</span><span class="sxs-lookup"><span data-stu-id="e8c48-123">Register the connector using a token created offline</span></span>

### <a name="register-the-connector-using-a-windows-powershell-credential-object"></a><span data-ttu-id="e8c48-124">Registro del conector mediante un objeto de credenciales de Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="e8c48-124">Register the connector using a Windows PowerShell credential object</span></span>
1. <span data-ttu-id="e8c48-125">Ejecute este comando para crear el objeto de credenciales de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e8c48-125">Create the Windows PowerShell Credentials object by running this command.</span></span> <span data-ttu-id="e8c48-126">Reemplace *\<username\>* y *\<password\>* por el nombre de usuario y la contraseña para el directorio:</span><span class="sxs-lookup"><span data-stu-id="e8c48-126">Replace *\<username\>* and *\<password\>* with the username and password for your directory:</span></span>
   
        $User = "<username>"
        $PlainPassword = '<password>'
        $SecurePassword = $PlainPassword | ConvertTo-SecureString -AsPlainText -Force
        $cred = New-Object –TypeName System.Management.Automation.PSCredential –ArgumentList $User, $SecurePassword
2. <span data-ttu-id="e8c48-127">Vaya a **C:\Archivos de programa\Microsoft AAD App Proxy Connector** y ejecute el script con el objeto de credenciales de PowerShell que creó.</span><span class="sxs-lookup"><span data-stu-id="e8c48-127">Go to **C:\Program Files\Microsoft AAD App Proxy Connector** and run the script using the PowerShell credentials object you created.</span></span> <span data-ttu-id="e8c48-128">Reemplace *$cred* por el nombre del objeto de credenciales de PowerShell que creó:</span><span class="sxs-lookup"><span data-stu-id="e8c48-128">Replace *$cred* with the name of the PowerShell credentials object you created:</span></span>
   
        RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Credentials -Usercredentials $cred

### <a name="register-the-connector-using-a-token-created-offline"></a><span data-ttu-id="e8c48-129">Registro del conector mediante un token creado sin conexión</span><span class="sxs-lookup"><span data-stu-id="e8c48-129">Register the connector using a token created offline</span></span>
1. <span data-ttu-id="e8c48-130">Cree un token sin conexión mediante la clase AuthenticationContext con los valores del código, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e8c48-130">Create an offline token using the AuthenticationContext class using the values in the code snippet:</span></span>

        using System;
        using System.Diagnostics;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;

        class Program
        {
        #region constants
        /// <summary>
        /// The AAD authentication endpoint uri
        /// </summary>
        static readonly Uri AadAuthenticationEndpoint = new Uri("https://login.microsoftonline.com/common/oauth2/token?api-version=1.0");

        /// <summary>
        /// The application ID of the connector in AAD
        /// </summary>
        static readonly string ConnectorAppId = "55747057-9b5d-4bd4-b387-abf52a8bd489";

        /// <summary>
        /// The reply address of the connector application in AAD
        /// </summary>
        static readonly Uri ConnectorRedirectAddress = new Uri("urn:ietf:wg:oauth:2.0:oob");

        /// <summary>
        /// The AppIdUri of the registration service in AAD
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


2. <span data-ttu-id="e8c48-131">Una vez que tenga el token, cree SecureString con dicho token:</span><span class="sxs-lookup"><span data-stu-id="e8c48-131">Once you have the token, create a SecureString using the token:</span></span>

   `$SecureToken = $Token | ConvertTo-SecureString -AsPlainText -Force`

3. <span data-ttu-id="e8c48-132">Ejecute el siguiente comando de Windows PowerShell, reemplazando \<tenant GUID\> por su identificador de directorio:</span><span class="sxs-lookup"><span data-stu-id="e8c48-132">Run the following Windows PowerShell command, replacing \<tenant GUID\> with your directory ID:</span></span>

   `RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Token -Token $SecureToken -TenantId <tenant GUID>`

## <a name="next-steps"></a><span data-ttu-id="e8c48-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e8c48-133">Next steps</span></span> 
* [<span data-ttu-id="e8c48-134">Publicar aplicaciones mediante su propio nombre de dominio</span><span class="sxs-lookup"><span data-stu-id="e8c48-134">Publish applications using your own domain name</span></span>](active-directory-application-proxy-custom-domains.md)
* [<span data-ttu-id="e8c48-135">Habilitar el inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="e8c48-135">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
* [<span data-ttu-id="e8c48-136">Solucionar los problemas que tiene con el Proxy de aplicación</span><span class="sxs-lookup"><span data-stu-id="e8c48-136">Troubleshoot issues you're having with Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)


