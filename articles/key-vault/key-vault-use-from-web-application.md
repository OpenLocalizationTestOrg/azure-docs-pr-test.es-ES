---
title: "Almacén de claves de Azure desde una aplicación Web aaaUse | Documentos de Microsoft"
description: "Use este tutorial toohelp aprenderá cómo toouse almacén de claves de Azure desde una aplicación web."
services: key-vault
documentationcenter: 
author: adhurwit
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 9b7d065e-1979-4397-8298-eeba3aec4792
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: adhurwit
ms.openlocfilehash: d5e2299e60b379c4e234d5cd6be03411c5a5c958
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-key-vault-from-a-web-application"></a><span data-ttu-id="991bb-103">Uso del Almacén de claves de Azure desde una aplicación web</span><span class="sxs-lookup"><span data-stu-id="991bb-103">Use Azure Key Vault from a Web Application</span></span>
## <a name="introduction"></a><span data-ttu-id="991bb-104">Introducción</span><span class="sxs-lookup"><span data-stu-id="991bb-104">Introduction</span></span>
<span data-ttu-id="991bb-105">Use este tutorial toohelp aprenderá cómo toouse almacén de claves de Azure desde una aplicación web en Azure.</span><span class="sxs-lookup"><span data-stu-id="991bb-105">Use this tutorial toohelp you learn how toouse Azure Key Vault from a web application in Azure.</span></span> <span data-ttu-id="991bb-106">Le guiará por el proceso de Hola de obtener acceso a un secreto desde un almacén de claves de Azure para que se puede utilizar en su aplicación web.</span><span class="sxs-lookup"><span data-stu-id="991bb-106">It walks you through hello process of accessing a secret from an Azure Key Vault so that it can be used in your web application.</span></span>

<span data-ttu-id="991bb-107">**Estimado toocomplete de tiempo:** 15 minutos</span><span class="sxs-lookup"><span data-stu-id="991bb-107">**Estimated time toocomplete:** 15 minutes</span></span>

<span data-ttu-id="991bb-108">Para obtener información general sobre el Almacén de claves de Azure, consulte [¿Qué es el Almacén de clave de Azure?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="991bb-108">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="991bb-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="991bb-109">Prerequisites</span></span>
<span data-ttu-id="991bb-110">toocomplete este tutorial, debe tener Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="991bb-110">toocomplete this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="991bb-111">Un secreto de tooa URI en un almacén de claves de Azure</span><span class="sxs-lookup"><span data-stu-id="991bb-111">A URI tooa secret in an Azure Key Vault</span></span>
* <span data-ttu-id="991bb-112">Un identificador de cliente y un secreto de cliente para una aplicación web se registran con Azure Active Directory que tiene acceso tooyour el almacén de claves</span><span class="sxs-lookup"><span data-stu-id="991bb-112">A Client ID and a Client Secret for a web application registered with Azure Active Directory that has access tooyour Key Vault</span></span>
* <span data-ttu-id="991bb-113">Una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="991bb-113">A web application.</span></span> <span data-ttu-id="991bb-114">Mostraremos pasos Hola para una aplicación de ASP.NET MVC implementada en Azure como una aplicación Web.</span><span class="sxs-lookup"><span data-stu-id="991bb-114">We will be showing hello steps for an ASP.NET MVC application deployed in Azure as a Web App.</span></span>

> [!NOTE]
> <span data-ttu-id="991bb-115">Es fundamental que ha completado los pasos de hello enumerados en [empezar a trabajar con el almacén de claves de Azure](key-vault-get-started.md) para este tutorial para que tenga Hola URI tooa secreto y Hola Id. de cliente y cliente para una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="991bb-115">It is essential that you have completed hello steps listed in [Get Started with Azure Key Vault](key-vault-get-started.md) for this tutorial so that you have hello URI tooa secret and hello Client ID and Client Secret for a web application.</span></span>
> 
> 

<span data-ttu-id="991bb-116">aplicación web de Hola que accederá a Hola el almacén de claves es Hola uno que está registrado en Azure Active Directory y se le han otorgado acceso tooyour el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="991bb-116">hello web application that will be accessing hello Key Vault is hello one that is registered in Azure Active Directory and has been given access tooyour Key Vault.</span></span> <span data-ttu-id="991bb-117">Si este no es el caso de hello, volver atrás tooRegister una aplicación en el tutorial de introducción de Hola y repita los pasos de hello indicados.</span><span class="sxs-lookup"><span data-stu-id="991bb-117">If this is not hello case, go back tooRegister an Application in hello Get Started tutorial and repeat hello steps listed.</span></span>

<span data-ttu-id="991bb-118">Este tutorial está diseñado para los desarrolladores web que entienda los fundamentos de hello de la creación de aplicaciones web en Azure.</span><span class="sxs-lookup"><span data-stu-id="991bb-118">This tutorial is designed for web developers that understand hello basics of creating web applications on Azure.</span></span> <span data-ttu-id="991bb-119">Para obtener más información sobre las aplicaciones web de Azure, consulte [Información general de aplicaciones web](../app-service-web/app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="991bb-119">For more information about Azure Web Apps, see [Web Apps overview](../app-service-web/app-service-web-overview.md).</span></span>

## <span data-ttu-id="991bb-120"><a id="packages"></a>Incorporación de paquetes NuGet</span><span class="sxs-lookup"><span data-stu-id="991bb-120"><a id="packages"></a>Add Nuget Packages</span></span>
<span data-ttu-id="991bb-121">Hay dos paquetes de la aplicación web necesita toohave instalado.</span><span class="sxs-lookup"><span data-stu-id="991bb-121">There are two packages that your web application needs toohave installed.</span></span>

* <span data-ttu-id="991bb-122">Biblioteca de autenticación de Active Directory: contiene métodos para interactuar con Azure Active Directory y administrar la identidad de usuario.</span><span class="sxs-lookup"><span data-stu-id="991bb-122">Active Directory Authentication Library - contains methods for interacting with Azure Active Directory and managing user identity</span></span>
* <span data-ttu-id="991bb-123">Biblioteca de Almacén claves de Azure:  contiene métodos para interactuar con el Almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="991bb-123">Azure Key Vault Library - contains methods for interacting with Azure Key Vault</span></span>

<span data-ttu-id="991bb-124">Ambos de estos paquetes se pueden instalar mediante Hola consola de administrador de paquetes mediante el comando Install-Package de Hola.</span><span class="sxs-lookup"><span data-stu-id="991bb-124">Both of these packages can be installed using hello Package Manager Console using hello Install-Package command.</span></span>

    // this is currently hello latest stable version of ADAL
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

    Install-Package Microsoft.Azure.KeyVault


## <span data-ttu-id="991bb-125"><a id="webconfig"></a>Modificación de Web.Config</span><span class="sxs-lookup"><span data-stu-id="991bb-125"><a id="webconfig"></a>Modify Web.Config</span></span>
<span data-ttu-id="991bb-126">Hay tres opciones de aplicación que necesitan el archivo web.config de toobe toohello agregada como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="991bb-126">There are three application settings that need toobe added toohello web.config file as follows.</span></span>

    <!-- ClientId and ClientSecret refer toohello web application registration with Azure Active Directory -->
    <add key="ClientId" value="clientid" />
    <add key="ClientSecret" value="clientsecret" />

    <!-- SecretUri is hello URI for hello secret in Azure Key Vault -->
    <add key="SecretUri" value="secreturi" />


<span data-ttu-id="991bb-127">Si no va toohost la aplicación como una aplicación Web de Azure, debe agregar Hola real ClientId, un secreto de cliente y secreto URI valores toohello web.config. De lo contrario, deje estos valores ficticios porque iremos agregando los valores reales de Hola Hola Portal de Azure para un nivel adicional de seguridad.</span><span class="sxs-lookup"><span data-stu-id="991bb-127">If you are not going toohost your application as an Azure Web App, then you should add hello actual ClientId, Client Secret, and Secret URI values toohello web.config. Otherwise leave these dummy values because we will be adding hello actual values in hello Azure Portal for an additional level of security.</span></span>

## <span data-ttu-id="991bb-128"><a id="gettoken"></a>Agregar método tooGet un Token de acceso</span><span class="sxs-lookup"><span data-stu-id="991bb-128"><a id="gettoken"></a>Add Method tooGet an Access Token</span></span>
<span data-ttu-id="991bb-129">Hola de orden toouse API almacén de claves necesita un token de acceso.</span><span class="sxs-lookup"><span data-stu-id="991bb-129">In order toouse hello Key Vault API you need an access token.</span></span> <span data-ttu-id="991bb-130">Hola clave almacén cliente controla las llamadas toohello API almacén de claves pero debe toosupply con una función que obtiene el token de acceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="991bb-130">hello Key Vault Client handles calls toohello Key Vault API but you need toosupply it with a function that gets hello access token.</span></span>  

<span data-ttu-id="991bb-131">Aquí te mostramos Hola código tooget un token de acceso de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="991bb-131">Following is hello code tooget an access token from Azure Active Directory.</span></span> <span data-ttu-id="991bb-132">Este código puede estar en cualquier parte de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="991bb-132">This code can go anywhere in your application.</span></span> <span data-ttu-id="991bb-133">Me gusta tooadd un Utils o clase EncryptionHelper.</span><span class="sxs-lookup"><span data-stu-id="991bb-133">I like tooadd a Utils or EncryptionHelper class.</span></span>  

    //add these using statements
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using System.Threading.Tasks;
    using System.Web.Configuration;

    //this is an optional property toohold hello secret after it is retrieved
    public static string EncryptSecret { get; set; }

    //hello method that will be provided toohello KeyVaultClient
    public static async Task<string> GetToken(string authority, string resource, string scope)
    {
        var authContext = new AuthenticationContext(authority);
        ClientCredential clientCred = new ClientCredential(WebConfigurationManager.AppSettings["ClientId"],
                    WebConfigurationManager.AppSettings["ClientSecret"]);
        AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

        if (result == null)
            throw new InvalidOperationException("Failed tooobtain hello JWT token");

        return result.AccessToken;
    }

> [!NOTE]
> <span data-ttu-id="991bb-134">Mediante un identificador de cliente y el secreto del cliente es tooauthenticate de manera más fácil de hello una aplicación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="991bb-134">Using a Client ID and Client Secret is hello easiest way tooauthenticate an Azure AD application.</span></span> <span data-ttu-id="991bb-135">Y su uso en una aplicación web permite la separación de deberes y proporciona mayor control sobre la administración de claves.</span><span class="sxs-lookup"><span data-stu-id="991bb-135">And using it in your web application allows for a separation of duties and more control over your key management.</span></span> <span data-ttu-id="991bb-136">Pero se basan en la puesta Hola secreto de cliente en las opciones de configuración que para algunos pueden ser peligrosos como como colocar secreto Hola que desee tooprotect en las opciones de configuración.</span><span class="sxs-lookup"><span data-stu-id="991bb-136">But it does rely on putting hello Client Secret in your configuration settings which for some can be as risky as putting hello secret that you want tooprotect in your configuration settings.</span></span> <span data-ttu-id="991bb-137">Vea a continuación para obtener información sobre cómo toouse un identificador de cliente y un certificado en lugar de Id. de cliente y el secreto del cliente tooauthenticate Hola aplicación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="991bb-137">See below for a discussion on how toouse a Client ID and Certificate instead of Client ID and Client Secret tooauthenticate hello Azure AD application.</span></span>
> 
> 

## <span data-ttu-id="991bb-138"><a id="appstart"></a>Recuperar el secreto de hello en Iniciar aplicación</span><span class="sxs-lookup"><span data-stu-id="991bb-138"><a id="appstart"></a>Retrieve hello secret on Application Start</span></span>
<span data-ttu-id="991bb-139">Ahora necesitamos toocall Hola API almacén de claves de código y recuperar Hola secreto.</span><span class="sxs-lookup"><span data-stu-id="991bb-139">Now we need code toocall hello Key Vault API and retrieve hello secret.</span></span> <span data-ttu-id="991bb-140">Hello código siguiente se puede colocar en cualquier lugar mientras se llama antes de que necesites toouse lo.</span><span class="sxs-lookup"><span data-stu-id="991bb-140">hello following code can be put anywhere as long as it is called before you need toouse it.</span></span> <span data-ttu-id="991bb-141">He colocar este código en el evento de inicio de la aplicación de Hola Hola Global.asax para que se ejecuta una vez en el inicio y hace Hola secreto disponible para la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="991bb-141">I have put this code in hello Application Start event in hello Global.asax so that it runs once on start and makes hello secret available for hello application.</span></span>

    //add these using statements
    using Microsoft.Azure.KeyVault;
    using System.Web.Configuration;

    // I put my GetToken method in a Utils class. Change for wherever you placed your method.
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

    var sec = await kv.GetSecretAsync(WebConfigurationManager.AppSettings["SecretUri"]);

    //I put a variable in a Utils class toohold hello secret for general  application use.
    Utils.EncryptSecret = sec.Value;



## <span data-ttu-id="991bb-142"><a id="portalsettings"></a>Agregar configuración de la aplicación Hola Portal de Azure (opcional)</span><span class="sxs-lookup"><span data-stu-id="991bb-142"><a id="portalsettings"></a>Add App Settings in hello Azure Portal (optional)</span></span>
<span data-ttu-id="991bb-143">Si tiene una aplicación Web de Azure ahora puede agregar los valores reales para hello AppSettings Hola Hola Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="991bb-143">If you have an Azure Web App you can now add hello actual values for hello AppSettings in hello Azure Portal.</span></span> <span data-ttu-id="991bb-144">Al hacerlo, los valores reales de hello no estará en el archivo web.config de hello pero protegido a través de hello Portal donde tiene capacidades de control de acceso independientes.</span><span class="sxs-lookup"><span data-stu-id="991bb-144">By doing this, hello actual values will not be in hello web.config but protected via hello Portal where you have separate access control capabilities.</span></span> <span data-ttu-id="991bb-145">Estos valores se sustituirán por valores de hello que escribió en el archivo web.config. Asegúrese de que los nombres de Hola se Hola igual.</span><span class="sxs-lookup"><span data-stu-id="991bb-145">These values will be substituted for hello values that you entered in your web.config. Make sure that hello names are hello same.</span></span>

![Configuración de la aplicación mostrada en el Portal de Azure][1]

## <a name="authenticate-with-a-certificate-instead-of-a-client-secret"></a><span data-ttu-id="991bb-147">Autenticación con un certificado, en lugar de con un secreto de cliente</span><span class="sxs-lookup"><span data-stu-id="991bb-147">Authenticate with a Certificate instead of a Client Secret</span></span>
<span data-ttu-id="991bb-148">Es otra manera tooauthenticate una aplicación de Azure AD mediante un identificador de cliente y un certificado en lugar de un identificador de cliente y el secreto del cliente.</span><span class="sxs-lookup"><span data-stu-id="991bb-148">Another way tooauthenticate an Azure AD application is by using a Client ID and a Certificate instead of a Client ID and Client Secret.</span></span> <span data-ttu-id="991bb-149">A continuación se Hola pasos toouse un certificado en una aplicación Web de Azure:</span><span class="sxs-lookup"><span data-stu-id="991bb-149">Following are hello steps toouse a Certificate in an Azure Web App:</span></span>

1. <span data-ttu-id="991bb-150">Obtener o crear un certificado</span><span class="sxs-lookup"><span data-stu-id="991bb-150">Get or Create a Certificate</span></span>
2. <span data-ttu-id="991bb-151">Asociar Hola certificado a una aplicación de Azure AD</span><span class="sxs-lookup"><span data-stu-id="991bb-151">Associate hello Certificate with an Azure AD application</span></span>
3. <span data-ttu-id="991bb-152">Agregar Hola de toouse de aplicación Web de código tooyour certificado</span><span class="sxs-lookup"><span data-stu-id="991bb-152">Add code tooyour Web App toouse hello Certificate</span></span>
4. <span data-ttu-id="991bb-153">Agregar una aplicación Web de tooyour de certificado</span><span class="sxs-lookup"><span data-stu-id="991bb-153">Add a Certificate tooyour Web App</span></span>

<span data-ttu-id="991bb-154">**Obtener o crear un certificado** Para nuestros propósito, crearemos un certificado de prueba.</span><span class="sxs-lookup"><span data-stu-id="991bb-154">**Get or Create a Certificate** For our purposes we will make a test certificate.</span></span> <span data-ttu-id="991bb-155">Aquí se muestran un par de comandos que puede usar en un símbolo del sistema para desarrolladores toocreate un certificado.</span><span class="sxs-lookup"><span data-stu-id="991bb-155">Here are a couple of commands that you can use in a Developer Command Prompt toocreate a certificate.</span></span> <span data-ttu-id="991bb-156">Cambiar toowhere de directorio que desea Hola cert archivos creados.</span><span class="sxs-lookup"><span data-stu-id="991bb-156">Change directory toowhere you want hello cert files created.</span></span>  <span data-ttu-id="991bb-157">Además, para hello apertura y cierre de la fecha del certificado de hello, usar hello fecha actual más 1 año.</span><span class="sxs-lookup"><span data-stu-id="991bb-157">Also, for hello beginning and ending date of hello certificate, use hello current date plus 1 year.</span></span>

    makecert -sv mykey.pvk -n "cn=KVWebApp" KVWebApp.cer -b 03/07/2017 -e 03/07/2018 -r
    pvk2pfx -pvk mykey.pvk -spc KVWebApp.cer -pfx KVWebApp.pfx -po test123

<span data-ttu-id="991bb-158">Tome nota de la fecha de finalización de Hola y la contraseña de Hola de hello .pfx (en este ejemplo: 31/07/2016 y test123).</span><span class="sxs-lookup"><span data-stu-id="991bb-158">Make note of hello end date and hello password for hello .pfx (in this example: 07/31/2016 and test123).</span></span> <span data-ttu-id="991bb-159">Las necesitará más adelante.</span><span class="sxs-lookup"><span data-stu-id="991bb-159">You will need them below.</span></span>

<span data-ttu-id="991bb-160">Para más información sobre cómo crear un certificado de prueba, vea [Procedimientos para crear su propio certificado de prueba](https://msdn.microsoft.com/library/ff699202.aspx)</span><span class="sxs-lookup"><span data-stu-id="991bb-160">For more information on creating a test certificate, see [How to: Create Your Own Test Certificate](https://msdn.microsoft.com/library/ff699202.aspx)</span></span>

<span data-ttu-id="991bb-161">**Hola asociar certificados con una aplicación de Azure AD** ahora que tiene un certificado, debe tooassociate con una aplicación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="991bb-161">**Associate hello Certificate with an Azure AD application** Now that you have a certificate, you need tooassociate it with an Azure AD application.</span></span> <span data-ttu-id="991bb-162">Actualmente, Hola Portal de Azure no admite este flujo de trabajo; Esto puede realizarse a través de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="991bb-162">Presently, hello Azure Portal does not support this workflow; this can be completed through PowerShell.</span></span> <span data-ttu-id="991bb-163">Ejecute hello siguiendo el certificado de hello tooassoicate de comandos con la aplicación hello Azure AD:</span><span class="sxs-lookup"><span data-stu-id="991bb-163">Run hello following commands tooassoicate hello certificate with hello Azure AD application:</span></span>

    $x509 = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2
    $x509.Import("C:\data\KVWebApp.cer")
    $credValue = [System.Convert]::ToBase64String($x509.GetRawCertData())

    # If you used different dates for makecert then adjust these values
    $now = [System.DateTime]::Now
    $yearfromnow = $now.AddYears(1)

    $adapp = New-AzureRmADApplication -DisplayName "KVWebApp" -HomePage "http://kvwebapp" -IdentifierUris "http://kvwebapp" -CertValue $credValue -StartDate $now -EndDate $yearfromnow

    $sp = New-AzureRmADServicePrincipal -ApplicationId $adapp.ApplicationId

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'contosokv' -ServicePrincipalName $sp.ServicePrincipalName -PermissionsToSecrets all -ResourceGroupName 'contosorg'

    # get hello thumbprint toouse in your app settings
    $x509.Thumbprint

<span data-ttu-id="991bb-164">Después de ejecutar estos comandos, puede ver la aplicación hello en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="991bb-164">After you have run these commands, you can see hello application in Azure AD.</span></span> <span data-ttu-id="991bb-165">Al buscar, asegúrese de que seleccionar "Aplicaciones que tiene mi compañía" en lugar de "Aplicaciones que usa mi compañía" en el cuadro de diálogo de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="991bb-165">When searching, ensure you select "Applications my company owns" instead of "Applications my company uses" in hello search dialog.</span></span>

<span data-ttu-id="991bb-166">vea toolearn más información acerca de los objetos de aplicación de Azure AD y objetos ServicePrincipal y [objetos de entidad de servicio y aplicación](../active-directory/active-directory-application-objects.md)</span><span class="sxs-lookup"><span data-stu-id="991bb-166">toolearn more about Azure AD Application Objects and ServicePrincipal Objects, see [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md)</span></span>

<span data-ttu-id="991bb-167">**Agregar Hola de toouse de aplicación Web de código tooyour certificado** ahora agregaremos tooaccess de aplicación Web de código tooyour Hola cert y usarlo para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="991bb-167">**Add code tooyour Web App toouse hello Certificate** Now we will add code tooyour Web App tooaccess hello cert and use it for authentication.</span></span>

<span data-ttu-id="991bb-168">En primer lugar hay cert de hello tooaccess de código.</span><span class="sxs-lookup"><span data-stu-id="991bb-168">First there is code tooaccess hello cert.</span></span>

    public static class CertificateHelper
    {
        public static X509Certificate2 FindCertificateByThumbprint(string findValue)
        {
            X509Store store = new X509Store(StoreName.My, StoreLocation.CurrentUser);
            try
            {
                store.Open(OpenFlags.ReadOnly);
                X509Certificate2Collection col = store.Certificates.Find(X509FindType.FindByThumbprint,
                    findValue, false); // Don't validate certs, since hello test root isn't installed.
                if (col == null || col.Count == 0)
                    return null;
                return col[0];
            }
            finally
            {
                store.Close();
            }
        }
    }


<span data-ttu-id="991bb-169">Tenga en cuenta que Hola StoreLocation es CurrentUser en lugar de LocalMachine.</span><span class="sxs-lookup"><span data-stu-id="991bb-169">Note that hello StoreLocation is CurrentUser instead of LocalMachine.</span></span> <span data-ttu-id="991bb-170">Y que se está proporcionando toohello 'false' Find (método) como estamos usando un certificado de prueba.</span><span class="sxs-lookup"><span data-stu-id="991bb-170">And that we are supplying 'false' toohello Find method because we are using a test cert.</span></span>

<span data-ttu-id="991bb-171">A continuación hay código que usa hello CertificateHelper y crea un ClientAssertionCertificate que es necesario para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="991bb-171">Next is code that uses hello CertificateHelper and creates a ClientAssertionCertificate which is needed for authentication.</span></span>

    public static ClientAssertionCertificate AssertionCert { get; set; }

    public static void GetCert()
    {
        var clientAssertionCertPfx = CertificateHelper.FindCertificateByThumbprint(WebConfigurationManager.AppSettings["thumbprint"]);
        AssertionCert = new ClientAssertionCertificate(WebConfigurationManager.AppSettings["clientid"], clientAssertionCertPfx);
    }


<span data-ttu-id="991bb-172">Aquí es Hola nuevo código tooget Hola token de acceso.</span><span class="sxs-lookup"><span data-stu-id="991bb-172">Here is hello new code tooget hello access token.</span></span> <span data-ttu-id="991bb-173">Esto reemplaza Hola GetToken (método) anterior.</span><span class="sxs-lookup"><span data-stu-id="991bb-173">This replaces hello GetToken method above.</span></span> <span data-ttu-id="991bb-174">Para su comodidad, le hemos dado un nombre diferente.</span><span class="sxs-lookup"><span data-stu-id="991bb-174">I have given it a different name for convenience.</span></span>

    public static async Task<string> GetAccessToken(string authority, string resource, string scope)
    {
        var context = new AuthenticationContext(authority, TokenCache.DefaultShared);
        var result = await context.AcquireTokenAsync(resource, AssertionCert);
        return result.AccessToken;
    }

<span data-ttu-id="991bb-175">Para facilitar su uso, hemos colocado todo este código en la clase Utils del proyecto de aplicación web.</span><span class="sxs-lookup"><span data-stu-id="991bb-175">I have put all of this code into my Web App project's Utils class for ease of use.</span></span>

<span data-ttu-id="991bb-176">último cambio de código de Hello es Hola método Application_Start.</span><span class="sxs-lookup"><span data-stu-id="991bb-176">hello last code change is in hello Application_Start method.</span></span> <span data-ttu-id="991bb-177">Primero necesitamos toocall Hola Hola de GetCert() método tooload ClientAssertionCertificate.</span><span class="sxs-lookup"><span data-stu-id="991bb-177">First we need toocall hello GetCert() method tooload hello ClientAssertionCertificate.</span></span> <span data-ttu-id="991bb-178">Y, a continuación, cambiamos el método de devolución de llamada de Hola que se proporciona al crear un nuevo KeyVaultClient.</span><span class="sxs-lookup"><span data-stu-id="991bb-178">And then we change hello callback method that we supply when creating a new KeyVaultClient.</span></span> <span data-ttu-id="991bb-179">Tenga en cuenta que esto reemplaza el código de hello que hemos tenido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="991bb-179">Note that this replaces hello code that we had above.</span></span>

    Utils.GetCert();
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetAccessToken));


<span data-ttu-id="991bb-180">**Agregar un certificado tooyour aplicación Web a través del Portal de Azure de Hola** agregar una aplicación Web de tooyour de certificado es un proceso de dos pasos simples.</span><span class="sxs-lookup"><span data-stu-id="991bb-180">**Add a Certificate tooyour Web App through hello Azure Portal** Adding a Certificate tooyour Web App is a simple two-step process.</span></span> <span data-ttu-id="991bb-181">En primer lugar, vaya toohello Portal de Azure y navegue tooyour aplicación Web.</span><span class="sxs-lookup"><span data-stu-id="991bb-181">First, go toohello Azure Portal and navigate tooyour Web App.</span></span> <span data-ttu-id="991bb-182">En la hoja de configuración de hello para la aplicación Web, haga clic en la entrada de Hola para "los dominios personalizados y SSL".</span><span class="sxs-lookup"><span data-stu-id="991bb-182">On hello Settings blade for your Web App, click on hello entry for "Custom domains and SSL".</span></span> <span data-ttu-id="991bb-183">En hello hoja que se abrirá, estarán hello tooupload capaz de certificado que haya creado anteriormente, KVWebApp.pfx, asegúrese de que recordar contraseña Hola Hola pfx.</span><span class="sxs-lookup"><span data-stu-id="991bb-183">On hello blade that opens you will be able tooupload hello Certificate that you created above, KVWebApp.pfx, make sure that you remember hello password for hello pfx.</span></span>

![Agregar una aplicación Web de certificado tooa Hola Portal de Azure][2]

<span data-ttu-id="991bb-185">última cosa que necesite toodo Hello es tooadd una aplicación Web que tiene el sitio Web de nombre de Hola de configuración de la aplicación tooyour\_carga\_certificados y un valor de *.</span><span class="sxs-lookup"><span data-stu-id="991bb-185">hello last thing that you need toodo is tooadd an Application Setting tooyour Web App that has hello name WEBSITE\_LOAD\_CERTIFICATES and a value of *.</span></span> <span data-ttu-id="991bb-186">Esto garantizará que se cargan todos los certificados.</span><span class="sxs-lookup"><span data-stu-id="991bb-186">This will ensure that all Certificates are loaded.</span></span> <span data-ttu-id="991bb-187">Si deseara Hola solo tooload certificados en los que se ha cargado, a continuación, puede especificar una lista separada por comas de sus huellas digitales.</span><span class="sxs-lookup"><span data-stu-id="991bb-187">If you wanted tooload only hello Certificates that you have uploaded, then you can enter a comma-separated list of their thumbprints.</span></span>

<span data-ttu-id="991bb-188">vea toolearn más acerca de cómo agregar una aplicación Web, de certificado tooa [con certificados en las aplicaciones de sitios Web de Azure](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/)</span><span class="sxs-lookup"><span data-stu-id="991bb-188">toolearn more about adding a Certificate tooa Web App, see [Using Certificates in Azure Websites Applications](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/)</span></span>

<span data-ttu-id="991bb-189">**Agregar un almacén de certificados tooKey como un secreto** en lugar de cargar el servicio de aplicación Web de certificado toohello directamente, también puede almacenar en el almacén de claves como un secreto e implementarlo desde allí.</span><span class="sxs-lookup"><span data-stu-id="991bb-189">**Add a Certificate tooKey Vault as a secret** Instead of uploading your certificate toohello Web App service directly, you can store it in Key Vault as a secret and deploy it from there.</span></span> <span data-ttu-id="991bb-190">Se trata de un proceso de dos pasos que se describe en hello después de la entrada de blog, [implementar certificado Azure la aplicación Web a través del almacén de claves](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)</span><span class="sxs-lookup"><span data-stu-id="991bb-190">This is a two-step process that is outlined in hello following blog post, [Deploying Azure Web App Certificate through Key Vault](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)</span></span>

## <span data-ttu-id="991bb-191"><a id="next"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="991bb-191"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="991bb-192">Para conocer las referencias de programación, consulte [Referencia de la API de cliente de C# del Almacén de claves](https://msdn.microsoft.com/library/azure/dn903628.aspx).</span><span class="sxs-lookup"><span data-stu-id="991bb-192">For programming references, see [Azure Key Vault C# Client API Reference](https://msdn.microsoft.com/library/azure/dn903628.aspx).</span></span>

<!--Image references-->
[1]: ./media/key-vault-use-from-web-application/PortalAppSettings.png
[2]: ./media/key-vault-use-from-web-application/PortalAddCertificate.png
