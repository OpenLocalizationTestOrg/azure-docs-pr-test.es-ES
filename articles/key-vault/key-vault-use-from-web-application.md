---
title: "Uso de Azure Key Vault desde una aplicación web | Microsoft Docs"
description: "Use este tutorial para ayudarle a aprender a usar el Almacén de claves de Azure desde una aplicación web."
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
ms.openlocfilehash: d095bcfe37baefa90cf79bb48bff3f703ce1dad7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-key-vault-from-a-web-application"></a><span data-ttu-id="634ac-103">Uso del Almacén de claves de Azure desde una aplicación web</span><span class="sxs-lookup"><span data-stu-id="634ac-103">Use Azure Key Vault from a Web Application</span></span>
## <a name="introduction"></a><span data-ttu-id="634ac-104">Introducción</span><span class="sxs-lookup"><span data-stu-id="634ac-104">Introduction</span></span>
<span data-ttu-id="634ac-105">Use este tutorial como ayuda para aprender a usar el Almacén de claves de Azure desde una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="634ac-105">Use this tutorial to help you learn how to use Azure Key Vault from a web application in Azure.</span></span> <span data-ttu-id="634ac-106">Le guiará por el proceso de obtener acceso a un secreto de un almacén de claves de Azure para que se pueda usar en su aplicación web.</span><span class="sxs-lookup"><span data-stu-id="634ac-106">It walks you through the process of accessing a secret from an Azure Key Vault so that it can be used in your web application.</span></span>

<span data-ttu-id="634ac-107">**Tiempo estimado para completar el tutorial:** 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="634ac-107">**Estimated time to complete:** 15 minutes</span></span>

<span data-ttu-id="634ac-108">Para obtener información general sobre el Almacén de claves de Azure, consulte [¿Qué es el Almacén de clave de Azure?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="634ac-108">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="634ac-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="634ac-109">Prerequisites</span></span>
<span data-ttu-id="634ac-110">Para realizar este tutorial, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="634ac-110">To complete this tutorial, you must have the following:</span></span>

* <span data-ttu-id="634ac-111">Un URI de un secreto en un almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="634ac-111">A URI to a secret in an Azure Key Vault</span></span>
* <span data-ttu-id="634ac-112">Un Id. de cliente y un secreto de cliente para una aplicación web registrada en Azure Active Directory que tenga acceso a su Almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="634ac-112">A Client ID and a Client Secret for a web application registered with Azure Active Directory that has access to your Key Vault</span></span>
* <span data-ttu-id="634ac-113">Una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="634ac-113">A web application.</span></span> <span data-ttu-id="634ac-114">Vamos a mostrarle los pasos para una aplicación ASP.NET MVC implementada en Azure como una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="634ac-114">We will be showing the steps for an ASP.NET MVC application deployed in Azure as a Web App.</span></span>

> [!NOTE]
> <span data-ttu-id="634ac-115">Para los fines de este tutorial, es esencial que haya realizado los pasos enumerados en [Introducción a Azure Key Vault](key-vault-get-started.md) para así disponer del URI de un secreto y del id. de cliente y el secreto de cliente de una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="634ac-115">It is essential that you have completed the steps listed in [Get Started with Azure Key Vault](key-vault-get-started.md) for this tutorial so that you have the URI to a secret and the Client ID and Client Secret for a web application.</span></span>
> 
> 

<span data-ttu-id="634ac-116">La aplicación web que va a tener acceso el Almacén de claves es la que está registrada en Azure Active Directory y a la que se le ha concedido para él.</span><span class="sxs-lookup"><span data-stu-id="634ac-116">The web application that will be accessing the Key Vault is the one that is registered in Azure Active Directory and has been given access to your Key Vault.</span></span> <span data-ttu-id="634ac-117">Si este no es el caso, vuelva al apartado sobre cómo registrar una aplicación del tutorial de introducción y repita los pasos enumerados.</span><span class="sxs-lookup"><span data-stu-id="634ac-117">If this is not the case, go back to Register an Application in the Get Started tutorial and repeat the steps listed.</span></span>

<span data-ttu-id="634ac-118">Este tutorial está diseñado para desarrolladores web que comprendan los conceptos básicos de la creación de aplicaciones web en Azure.</span><span class="sxs-lookup"><span data-stu-id="634ac-118">This tutorial is designed for web developers that understand the basics of creating web applications on Azure.</span></span> <span data-ttu-id="634ac-119">Para obtener más información sobre las aplicaciones web de Azure, consulte [Información general de aplicaciones web](../app-service-web/app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="634ac-119">For more information about Azure Web Apps, see [Web Apps overview](../app-service-web/app-service-web-overview.md).</span></span>

## <span data-ttu-id="634ac-120"><a id="packages"></a>Incorporación de paquetes NuGet</span><span class="sxs-lookup"><span data-stu-id="634ac-120"><a id="packages"></a>Add Nuget Packages</span></span>
<span data-ttu-id="634ac-121">Hay dos paquetes que la aplicación web debe tener instalados.</span><span class="sxs-lookup"><span data-stu-id="634ac-121">There are two packages that your web application needs to have installed.</span></span>

* <span data-ttu-id="634ac-122">Biblioteca de autenticación de Active Directory: contiene métodos para interactuar con Azure Active Directory y administrar la identidad de usuario.</span><span class="sxs-lookup"><span data-stu-id="634ac-122">Active Directory Authentication Library - contains methods for interacting with Azure Active Directory and managing user identity</span></span>
* <span data-ttu-id="634ac-123">Biblioteca de Almacén claves de Azure:  contiene métodos para interactuar con el Almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="634ac-123">Azure Key Vault Library - contains methods for interacting with Azure Key Vault</span></span>

<span data-ttu-id="634ac-124">Los dos paquetes se pueden instalar mediante la Consola del Administrador de paquetes con el comando Install-Package.</span><span class="sxs-lookup"><span data-stu-id="634ac-124">Both of these packages can be installed using the Package Manager Console using the Install-Package command.</span></span>

    // this is currently the latest stable version of ADAL
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

    Install-Package Microsoft.Azure.KeyVault


## <span data-ttu-id="634ac-125"><a id="webconfig"></a>Modificación de Web.Config</span><span class="sxs-lookup"><span data-stu-id="634ac-125"><a id="webconfig"></a>Modify Web.Config</span></span>
<span data-ttu-id="634ac-126">Hay tres configuraciones de aplicaciones que deben agregarse al archivo web.config como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="634ac-126">There are three application settings that need to be added to the web.config file as follows.</span></span>

    <!-- ClientId and ClientSecret refer to the web application registration with Azure Active Directory -->
    <add key="ClientId" value="clientid" />
    <add key="ClientSecret" value="clientsecret" />

    <!-- SecretUri is the URI for the secret in Azure Key Vault -->
    <add key="SecretUri" value="secreturi" />


<span data-ttu-id="634ac-127">Si no va a hospedar la aplicación como una aplicación web de Azure, debe agregar los valores reales de ClientId, Secreto de cliente y URI de secreto al web.config.</span><span class="sxs-lookup"><span data-stu-id="634ac-127">If you are not going to host your application as an Azure Web App, then you should add the actual ClientId, Client Secret, and Secret URI values to the web.config.</span></span> <span data-ttu-id="634ac-128">De lo contrario, deje estos valores ficticios porque iremos agregando los valores reales en el Portal de Azure para lograr un nivel de seguridad adicional.</span><span class="sxs-lookup"><span data-stu-id="634ac-128">Otherwise leave these dummy values because we will be adding the actual values in the Azure Portal for an additional level of security.</span></span>

## <span data-ttu-id="634ac-129"><a id="gettoken"></a>Agregar el método para obtener un token de acceso</span><span class="sxs-lookup"><span data-stu-id="634ac-129"><a id="gettoken"></a>Add Method to Get an Access Token</span></span>
<span data-ttu-id="634ac-130">Para usar la API del Almacén de claves necesita un token de acceso.</span><span class="sxs-lookup"><span data-stu-id="634ac-130">In order to use the Key Vault API you need an access token.</span></span> <span data-ttu-id="634ac-131">El cliente del Almacén de claves controla las llamadas a la API del Almacén de claves, pero deberá suministrarle una función que obtenga el token de acceso.</span><span class="sxs-lookup"><span data-stu-id="634ac-131">The Key Vault Client handles calls to the Key Vault API but you need to supply it with a function that gets the access token.</span></span>  

<span data-ttu-id="634ac-132">A continuación se muestra el código para obtener un token de acceso de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="634ac-132">Following is the code to get an access token from Azure Active Directory.</span></span> <span data-ttu-id="634ac-133">Este código puede estar en cualquier parte de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="634ac-133">This code can go anywhere in your application.</span></span> <span data-ttu-id="634ac-134">Quiero agregar una clase Utils o EncryptionHelper.</span><span class="sxs-lookup"><span data-stu-id="634ac-134">I like to add a Utils or EncryptionHelper class.</span></span>  

    //add these using statements
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using System.Threading.Tasks;
    using System.Web.Configuration;

    //this is an optional property to hold the secret after it is retrieved
    public static string EncryptSecret { get; set; }

    //the method that will be provided to the KeyVaultClient
    public static async Task<string> GetToken(string authority, string resource, string scope)
    {
        var authContext = new AuthenticationContext(authority);
        ClientCredential clientCred = new ClientCredential(WebConfigurationManager.AppSettings["ClientId"],
                    WebConfigurationManager.AppSettings["ClientSecret"]);
        AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

        if (result == null)
            throw new InvalidOperationException("Failed to obtain the JWT token");

        return result.AccessToken;
    }

> [!NOTE]
> <span data-ttu-id="634ac-135">La forma más sencilla de autenticar una aplicación de Azure AD es mediante un secreto de cliente y un identificador de cliente.</span><span class="sxs-lookup"><span data-stu-id="634ac-135">Using a Client ID and Client Secret is the easiest way to authenticate an Azure AD application.</span></span> <span data-ttu-id="634ac-136">Y su uso en una aplicación web permite la separación de deberes y proporciona mayor control sobre la administración de claves.</span><span class="sxs-lookup"><span data-stu-id="634ac-136">And using it in your web application allows for a separation of duties and more control over your key management.</span></span> <span data-ttu-id="634ac-137">Pero se basa en colocar el secreto de cliente en las opciones de configuración, lo que, para algunos, puede ser tan arriesgado como poner el secreto que se desea proteger en las opciones de configuración.</span><span class="sxs-lookup"><span data-stu-id="634ac-137">But it does rely on putting the Client Secret in your configuration settings which for some can be as risky as putting the secret that you want to protect in your configuration settings.</span></span> <span data-ttu-id="634ac-138">A continuación encontrará información sobre el uso de un Id. de cliente y un certificado, en lugar de un Id. de cliente y un secreto de cliente para autenticar la aplicación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="634ac-138">See below for a discussion on how to use a Client ID and Certificate instead of Client ID and Client Secret to authenticate the Azure AD application.</span></span>
> 
> 

## <span data-ttu-id="634ac-139"><a id="appstart"></a>Recuperación del secreto en Inicio de aplicación</span><span class="sxs-lookup"><span data-stu-id="634ac-139"><a id="appstart"></a>Retrieve the secret on Application Start</span></span>
<span data-ttu-id="634ac-140">Ahora tenemos el código para llamar a la API de Almacén de claves y recuperar el secreto.</span><span class="sxs-lookup"><span data-stu-id="634ac-140">Now we need code to call the Key Vault API and retrieve the secret.</span></span> <span data-ttu-id="634ac-141">El siguiente código se puede colocar en cualquier parte siempre que se llame antes de que sea necesario usarlo.</span><span class="sxs-lookup"><span data-stu-id="634ac-141">The following code can be put anywhere as long as it is called before you need to use it.</span></span> <span data-ttu-id="634ac-142">He colocado este código en el evento Inicio de aplicación en Global.asax para que se ejecute una vez en el inicio y permita que esté disponible el secreto para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="634ac-142">I have put this code in the Application Start event in the Global.asax so that it runs once on start and makes the secret available for the application.</span></span>

    //add these using statements
    using Microsoft.Azure.KeyVault;
    using System.Web.Configuration;

    // I put my GetToken method in a Utils class. Change for wherever you placed your method.
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

    var sec = await kv.GetSecretAsync(WebConfigurationManager.AppSettings["SecretUri"]);

    //I put a variable in a Utils class to hold the secret for general  application use.
    Utils.EncryptSecret = sec.Value;



## <span data-ttu-id="634ac-143"><a id="portalsettings"></a>Agregar la configuración de la aplicación en el Portal de Azure (opcional)</span><span class="sxs-lookup"><span data-stu-id="634ac-143"><a id="portalsettings"></a>Add App Settings in the Azure Portal (optional)</span></span>
<span data-ttu-id="634ac-144">Si tiene una aplicación web de Azure ahora puede agregar los valores reales para AppSettings en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="634ac-144">If you have an Azure Web App you can now add the actual values for the AppSettings in the Azure Portal.</span></span> <span data-ttu-id="634ac-145">De esta manera, los valores reales no estarán en web.config sino que estarán protegidos a través del Portal donde cuenta con capacidades de control de acceso independientes.</span><span class="sxs-lookup"><span data-stu-id="634ac-145">By doing this, the actual values will not be in the web.config but protected via the Portal where you have separate access control capabilities.</span></span> <span data-ttu-id="634ac-146">Estos valores se sustituirán por los valores que escribió en web.config.</span><span class="sxs-lookup"><span data-stu-id="634ac-146">These values will be substituted for the values that you entered in your web.config.</span></span> <span data-ttu-id="634ac-147">Asegúrese de que los nombres sean los mismos.</span><span class="sxs-lookup"><span data-stu-id="634ac-147">Make sure that the names are the same.</span></span>

![Configuración de la aplicación mostrada en el Portal de Azure][1]

## <a name="authenticate-with-a-certificate-instead-of-a-client-secret"></a><span data-ttu-id="634ac-149">Autenticación con un certificado, en lugar de con un secreto de cliente</span><span class="sxs-lookup"><span data-stu-id="634ac-149">Authenticate with a Certificate instead of a Client Secret</span></span>
<span data-ttu-id="634ac-150">Otra forma de autenticar una aplicación de Azure AD es mediante el uso de un Id. de cliente y un certificado, en lugar de un Id. de cliente y un secreto de cliente.</span><span class="sxs-lookup"><span data-stu-id="634ac-150">Another way to authenticate an Azure AD application is by using a Client ID and a Certificate instead of a Client ID and Client Secret.</span></span> <span data-ttu-id="634ac-151">Estos son los pasos necesarios para usar un certificado en una aplicación web de Azure:</span><span class="sxs-lookup"><span data-stu-id="634ac-151">Following are the steps to use a Certificate in an Azure Web App:</span></span>

1. <span data-ttu-id="634ac-152">Obtener o crear un certificado</span><span class="sxs-lookup"><span data-stu-id="634ac-152">Get or Create a Certificate</span></span>
2. <span data-ttu-id="634ac-153">Asociar el certificado a una aplicación de Azure AD</span><span class="sxs-lookup"><span data-stu-id="634ac-153">Associate the Certificate with an Azure AD application</span></span>
3. <span data-ttu-id="634ac-154">Agregar código a la aplicación web para que use el certificado</span><span class="sxs-lookup"><span data-stu-id="634ac-154">Add code to your Web App to use the Certificate</span></span>
4. <span data-ttu-id="634ac-155">Agregar un certificado a la aplicación web</span><span class="sxs-lookup"><span data-stu-id="634ac-155">Add a Certificate to your Web App</span></span>

<span data-ttu-id="634ac-156">**Obtener o crear un certificado** Para nuestros propósito, crearemos un certificado de prueba.</span><span class="sxs-lookup"><span data-stu-id="634ac-156">**Get or Create a Certificate** For our purposes we will make a test certificate.</span></span> <span data-ttu-id="634ac-157">A continuación encontrará un par de comandos que se pueden usar en un símbolo del sistema para desarrolladores para crear un certificado.</span><span class="sxs-lookup"><span data-stu-id="634ac-157">Here are a couple of commands that you can use in a Developer Command Prompt to create a certificate.</span></span> <span data-ttu-id="634ac-158">Cambie al directorio a aquel en el que desea que se creen los archivos de certificado.</span><span class="sxs-lookup"><span data-stu-id="634ac-158">Change directory to where you want the cert files created.</span></span>  <span data-ttu-id="634ac-159">Además, para las fechas de inicio y fin del certificado, utilice la fecha actual más 1 año.</span><span class="sxs-lookup"><span data-stu-id="634ac-159">Also, for the beginning and ending date of the certificate, use the current date plus 1 year.</span></span>

    makecert -sv mykey.pvk -n "cn=KVWebApp" KVWebApp.cer -b 03/07/2017 -e 03/07/2018 -r
    pvk2pfx -pvk mykey.pvk -spc KVWebApp.cer -pfx KVWebApp.pfx -po test123

<span data-ttu-id="634ac-160">Tome nota de la fecha de finalización y la contraseña del archivo .pfx (en este ejemplo: 31/07/2016 y test123).</span><span class="sxs-lookup"><span data-stu-id="634ac-160">Make note of the end date and the password for the .pfx (in this example: 07/31/2016 and test123).</span></span> <span data-ttu-id="634ac-161">Las necesitará más adelante.</span><span class="sxs-lookup"><span data-stu-id="634ac-161">You will need them below.</span></span>

<span data-ttu-id="634ac-162">Para más información sobre cómo crear un certificado de prueba, vea [Procedimientos para crear su propio certificado de prueba](https://msdn.microsoft.com/library/ff699202.aspx)</span><span class="sxs-lookup"><span data-stu-id="634ac-162">For more information on creating a test certificate, see [How to: Create Your Own Test Certificate](https://msdn.microsoft.com/library/ff699202.aspx)</span></span>

<span data-ttu-id="634ac-163">**Asociar el certificado a una aplicación de Azure AD** Ahora que tiene un certificado, tendrá que asociarlo a una aplicación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="634ac-163">**Associate the Certificate with an Azure AD application** Now that you have a certificate, you need to associate it with an Azure AD application.</span></span> <span data-ttu-id="634ac-164">Actualmente, Azure Portal no admite este flujo de trabajo; esto puede realizarse mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="634ac-164">Presently, the Azure Portal does not support this workflow; this can be completed through PowerShell.</span></span> <span data-ttu-id="634ac-165">Ejecute los siguientes comandos para asociar el certificado con la aplicación de Azure AD:</span><span class="sxs-lookup"><span data-stu-id="634ac-165">Run the following commands to assoicate the certificate with the Azure AD application:</span></span>

    $x509 = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2
    $x509.Import("C:\data\KVWebApp.cer")
    $credValue = [System.Convert]::ToBase64String($x509.GetRawCertData())

    # If you used different dates for makecert then adjust these values
    $now = [System.DateTime]::Now
    $yearfromnow = $now.AddYears(1)

    $adapp = New-AzureRmADApplication -DisplayName "KVWebApp" -HomePage "http://kvwebapp" -IdentifierUris "http://kvwebapp" -CertValue $credValue -StartDate $now -EndDate $yearfromnow

    $sp = New-AzureRmADServicePrincipal -ApplicationId $adapp.ApplicationId

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'contosokv' -ServicePrincipalName $sp.ServicePrincipalName -PermissionsToSecrets all -ResourceGroupName 'contosorg'

    # get the thumbprint to use in your app settings
    $x509.Thumbprint

<span data-ttu-id="634ac-166">Después de ejecutar estos comandos, podrá ver la aplicación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="634ac-166">After you have run these commands, you can see the application in Azure AD.</span></span> <span data-ttu-id="634ac-167">Al buscar, asegúrese de que seleccionar "Aplicaciones que tiene mi compañía" en lugar de "Aplicaciones que usa mi compañía" en el cuadro de diálogo de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="634ac-167">When searching, ensure you select "Applications my company owns" instead of "Applications my company uses" in the search dialog.</span></span>

<span data-ttu-id="634ac-168">Para obtener más información acerca de los objetos Application y los objetos  ServicePrincipal de Azure AD, consulte [Objetos Application y objetos ServicePrincipal](../active-directory/active-directory-application-objects.md)</span><span class="sxs-lookup"><span data-stu-id="634ac-168">To learn more about Azure AD Application Objects and ServicePrincipal Objects, see [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md)</span></span>

<span data-ttu-id="634ac-169">**Agregar código a la aplicación web para que use el certificado** Ahora agregaremos código a la aplicación web para tener acceso al certificado y usarlo para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="634ac-169">**Add code to your Web App to use the Certificate** Now we will add code to your Web App to access the cert and use it for authentication.</span></span>

<span data-ttu-id="634ac-170">En primer lugar, este es el código para tener acceso al certificado.</span><span class="sxs-lookup"><span data-stu-id="634ac-170">First there is code to access the cert.</span></span>

    public static class CertificateHelper
    {
        public static X509Certificate2 FindCertificateByThumbprint(string findValue)
        {
            X509Store store = new X509Store(StoreName.My, StoreLocation.CurrentUser);
            try
            {
                store.Open(OpenFlags.ReadOnly);
                X509Certificate2Collection col = store.Certificates.Find(X509FindType.FindByThumbprint,
                    findValue, false); // Don't validate certs, since the test root isn't installed.
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


<span data-ttu-id="634ac-171">Observe que StoreLocation es CurrentUser, en lugar de LocalMachine.</span><span class="sxs-lookup"><span data-stu-id="634ac-171">Note that the StoreLocation is CurrentUser instead of LocalMachine.</span></span> <span data-ttu-id="634ac-172">Fíjese también en que usamos 'false' en el método Find, ya que usamos un certificado de prueba.</span><span class="sxs-lookup"><span data-stu-id="634ac-172">And that we are supplying 'false' to the Find method because we are using a test cert.</span></span>

<span data-ttu-id="634ac-173">El siguiente código usa CertificateHelper y crea ClientAssertionCertificate, que es necesario para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="634ac-173">Next is code that uses the CertificateHelper and creates a ClientAssertionCertificate which is needed for authentication.</span></span>

    public static ClientAssertionCertificate AssertionCert { get; set; }

    public static void GetCert()
    {
        var clientAssertionCertPfx = CertificateHelper.FindCertificateByThumbprint(WebConfigurationManager.AppSettings["thumbprint"]);
        AssertionCert = new ClientAssertionCertificate(WebConfigurationManager.AppSettings["clientid"], clientAssertionCertPfx);
    }


<span data-ttu-id="634ac-174">Este es el nuevo código para obtener el token de acceso.</span><span class="sxs-lookup"><span data-stu-id="634ac-174">Here is the new code to get the access token.</span></span> <span data-ttu-id="634ac-175">Reemplaza el método GetToken anterior.</span><span class="sxs-lookup"><span data-stu-id="634ac-175">This replaces the GetToken method above.</span></span> <span data-ttu-id="634ac-176">Para su comodidad, le hemos dado un nombre diferente.</span><span class="sxs-lookup"><span data-stu-id="634ac-176">I have given it a different name for convenience.</span></span>

    public static async Task<string> GetAccessToken(string authority, string resource, string scope)
    {
        var context = new AuthenticationContext(authority, TokenCache.DefaultShared);
        var result = await context.AcquireTokenAsync(resource, AssertionCert);
        return result.AccessToken;
    }

<span data-ttu-id="634ac-177">Para facilitar su uso, hemos colocado todo este código en la clase Utils del proyecto de aplicación web.</span><span class="sxs-lookup"><span data-stu-id="634ac-177">I have put all of this code into my Web App project's Utils class for ease of use.</span></span>

<span data-ttu-id="634ac-178">El último cambio de código se da en el método Application_Start.</span><span class="sxs-lookup"><span data-stu-id="634ac-178">The last code change is in the Application_Start method.</span></span> <span data-ttu-id="634ac-179">En primer lugar, es preciso llamar al método GetCert() para cargar ClientAssertionCertificate.</span><span class="sxs-lookup"><span data-stu-id="634ac-179">First we need to call the GetCert() method to load the ClientAssertionCertificate.</span></span> <span data-ttu-id="634ac-180">Y, a continuación, se cambia el método de devolución de llamada que se suministra al crear un nuevo KeyVaultClient.</span><span class="sxs-lookup"><span data-stu-id="634ac-180">And then we change the callback method that we supply when creating a new KeyVaultClient.</span></span> <span data-ttu-id="634ac-181">Tenga en cuenta que esto reemplazará el código anterior.</span><span class="sxs-lookup"><span data-stu-id="634ac-181">Note that this replaces the code that we had above.</span></span>

    Utils.GetCert();
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetAccessToken));


<span data-ttu-id="634ac-182">**Agregar un certificado a la aplicación web a través del Portal de Azure** La adición de un certificado a una aplicación web es un sencillo proceso de dos pasos.</span><span class="sxs-lookup"><span data-stu-id="634ac-182">**Add a Certificate to your Web App through the Azure Portal** Adding a Certificate to your Web App is a simple two-step process.</span></span> <span data-ttu-id="634ac-183">En primer lugar, vaya al Portal de Azure y navegue a la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="634ac-183">First, go to the Azure Portal and navigate to your Web App.</span></span> <span data-ttu-id="634ac-184">En la hoja Configuración de la aplicación web, haga clic en la entrada de "Dominios personalizados y SSL".</span><span class="sxs-lookup"><span data-stu-id="634ac-184">On the Settings blade for your Web App, click on the entry for "Custom domains and SSL".</span></span> <span data-ttu-id="634ac-185">En la hoja que se abre podrá cargar el certificado que creó anteriormente, KVWebApp.pfx, asegúrese de que recuerda la contraseña del archivo pfx.</span><span class="sxs-lookup"><span data-stu-id="634ac-185">On the blade that opens you will be able to upload the Certificate that you created above, KVWebApp.pfx, make sure that you remember the password for the pfx.</span></span>

![Adición de un certificado a una aplicación web en el Portal de Azure][2]

<span data-ttu-id="634ac-187">Lo último que debe hacer es agregar una configuración de aplicación a la aplicación web cuyo nombre es WEBSITE\_LOAD\_CERTIFICATES y cuyo valor es *.</span><span class="sxs-lookup"><span data-stu-id="634ac-187">The last thing that you need to do is to add an Application Setting to your Web App that has the name WEBSITE\_LOAD\_CERTIFICATES and a value of *.</span></span> <span data-ttu-id="634ac-188">Esto garantizará que se cargan todos los certificados.</span><span class="sxs-lookup"><span data-stu-id="634ac-188">This will ensure that all Certificates are loaded.</span></span> <span data-ttu-id="634ac-189">Si desea cargar solo los certificados que ha cargado, puede escribir una lista separada por comas de sus huellas digitales.</span><span class="sxs-lookup"><span data-stu-id="634ac-189">If you wanted to load only the Certificates that you have uploaded, then you can enter a comma-separated list of their thumbprints.</span></span>

<span data-ttu-id="634ac-190">Para obtener más información sobre cómo agregar un certificado a una aplicación Web, consulte [Uso de certificados en las aplicaciones de Sitios web de Azure](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/)</span><span class="sxs-lookup"><span data-stu-id="634ac-190">To learn more about adding a Certificate to a Web App, see [Using Certificates in Azure Websites Applications](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/)</span></span>

<span data-ttu-id="634ac-191">**Agregue un certificado al almacén de claves como un secreto** En lugar de cargar el certificado directamente al servicio de aplicación web, puede almacenarlo en el almacén de claves como un secreto e implementarlo desde allí.</span><span class="sxs-lookup"><span data-stu-id="634ac-191">**Add a Certificate to Key Vault as a secret** Instead of uploading your certificate to the Web App service directly, you can store it in Key Vault as a secret and deploy it from there.</span></span> <span data-ttu-id="634ac-192">Este es un proceso de dos pasos que se describe en la siguiente entrada de blog [Deploying Azure Web App Certificate through Key Vault](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)</span><span class="sxs-lookup"><span data-stu-id="634ac-192">This is a two-step process that is outlined in the following blog post, [Deploying Azure Web App Certificate through Key Vault](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)</span></span>

## <span data-ttu-id="634ac-193"><a id="next"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="634ac-193"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="634ac-194">Para conocer las referencias de programación, consulte [Referencia de la API de cliente de C# del Almacén de claves](https://msdn.microsoft.com/library/azure/dn903628.aspx).</span><span class="sxs-lookup"><span data-stu-id="634ac-194">For programming references, see [Azure Key Vault C# Client API Reference](https://msdn.microsoft.com/library/azure/dn903628.aspx).</span></span>

<!--Image references-->
[1]: ./media/key-vault-use-from-web-application/PortalAppSettings.png
[2]: ./media/key-vault-use-from-web-application/PortalAddCertificate.png
