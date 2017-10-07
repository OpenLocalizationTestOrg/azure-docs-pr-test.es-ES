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
# <a name="use-azure-key-vault-from-a-web-application"></a>Uso del Almacén de claves de Azure desde una aplicación web
## <a name="introduction"></a>Introducción
Use este tutorial toohelp aprenderá cómo toouse almacén de claves de Azure desde una aplicación web en Azure. Le guiará por el proceso de Hola de obtener acceso a un secreto desde un almacén de claves de Azure para que se puede utilizar en su aplicación web.

**Estimado toocomplete de tiempo:** 15 minutos

Para obtener información general sobre el Almacén de claves de Azure, consulte [¿Qué es el Almacén de clave de Azure?](key-vault-whatis.md)

## <a name="prerequisites"></a>Requisitos previos
toocomplete este tutorial, debe tener Hola siguientes:

* Un secreto de tooa URI en un almacén de claves de Azure
* Un identificador de cliente y un secreto de cliente para una aplicación web se registran con Azure Active Directory que tiene acceso tooyour el almacén de claves
* Una aplicación web. Mostraremos pasos Hola para una aplicación de ASP.NET MVC implementada en Azure como una aplicación Web.

> [!NOTE]
> Es fundamental que ha completado los pasos de hello enumerados en [empezar a trabajar con el almacén de claves de Azure](key-vault-get-started.md) para este tutorial para que tenga Hola URI tooa secreto y Hola Id. de cliente y cliente para una aplicación web.
> 
> 

aplicación web de Hola que accederá a Hola el almacén de claves es Hola uno que está registrado en Azure Active Directory y se le han otorgado acceso tooyour el almacén de claves. Si este no es el caso de hello, volver atrás tooRegister una aplicación en el tutorial de introducción de Hola y repita los pasos de hello indicados.

Este tutorial está diseñado para los desarrolladores web que entienda los fundamentos de hello de la creación de aplicaciones web en Azure. Para obtener más información sobre las aplicaciones web de Azure, consulte [Información general de aplicaciones web](../app-service-web/app-service-web-overview.md).

## <a id="packages"></a>Incorporación de paquetes NuGet
Hay dos paquetes de la aplicación web necesita toohave instalado.

* Biblioteca de autenticación de Active Directory: contiene métodos para interactuar con Azure Active Directory y administrar la identidad de usuario.
* Biblioteca de Almacén claves de Azure:  contiene métodos para interactuar con el Almacén de claves de Azure.

Ambos de estos paquetes se pueden instalar mediante Hola consola de administrador de paquetes mediante el comando Install-Package de Hola.

    // this is currently hello latest stable version of ADAL
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

    Install-Package Microsoft.Azure.KeyVault


## <a id="webconfig"></a>Modificación de Web.Config
Hay tres opciones de aplicación que necesitan el archivo web.config de toobe toohello agregada como se indica a continuación.

    <!-- ClientId and ClientSecret refer toohello web application registration with Azure Active Directory -->
    <add key="ClientId" value="clientid" />
    <add key="ClientSecret" value="clientsecret" />

    <!-- SecretUri is hello URI for hello secret in Azure Key Vault -->
    <add key="SecretUri" value="secreturi" />


Si no va toohost la aplicación como una aplicación Web de Azure, debe agregar Hola real ClientId, un secreto de cliente y secreto URI valores toohello web.config. De lo contrario, deje estos valores ficticios porque iremos agregando los valores reales de Hola Hola Portal de Azure para un nivel adicional de seguridad.

## <a id="gettoken"></a>Agregar método tooGet un Token de acceso
Hola de orden toouse API almacén de claves necesita un token de acceso. Hola clave almacén cliente controla las llamadas toohello API almacén de claves pero debe toosupply con una función que obtiene el token de acceso de Hola.  

Aquí te mostramos Hola código tooget un token de acceso de Azure Active Directory. Este código puede estar en cualquier parte de la aplicación. Me gusta tooadd un Utils o clase EncryptionHelper.  

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
> Mediante un identificador de cliente y el secreto del cliente es tooauthenticate de manera más fácil de hello una aplicación de Azure AD. Y su uso en una aplicación web permite la separación de deberes y proporciona mayor control sobre la administración de claves. Pero se basan en la puesta Hola secreto de cliente en las opciones de configuración que para algunos pueden ser peligrosos como como colocar secreto Hola que desee tooprotect en las opciones de configuración. Vea a continuación para obtener información sobre cómo toouse un identificador de cliente y un certificado en lugar de Id. de cliente y el secreto del cliente tooauthenticate Hola aplicación de Azure AD.
> 
> 

## <a id="appstart"></a>Recuperar el secreto de hello en Iniciar aplicación
Ahora necesitamos toocall Hola API almacén de claves de código y recuperar Hola secreto. Hello código siguiente se puede colocar en cualquier lugar mientras se llama antes de que necesites toouse lo. He colocar este código en el evento de inicio de la aplicación de Hola Hola Global.asax para que se ejecuta una vez en el inicio y hace Hola secreto disponible para la aplicación hello.

    //add these using statements
    using Microsoft.Azure.KeyVault;
    using System.Web.Configuration;

    // I put my GetToken method in a Utils class. Change for wherever you placed your method.
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

    var sec = await kv.GetSecretAsync(WebConfigurationManager.AppSettings["SecretUri"]);

    //I put a variable in a Utils class toohold hello secret for general  application use.
    Utils.EncryptSecret = sec.Value;



## <a id="portalsettings"></a>Agregar configuración de la aplicación Hola Portal de Azure (opcional)
Si tiene una aplicación Web de Azure ahora puede agregar los valores reales para hello AppSettings Hola Hola Portal de Azure. Al hacerlo, los valores reales de hello no estará en el archivo web.config de hello pero protegido a través de hello Portal donde tiene capacidades de control de acceso independientes. Estos valores se sustituirán por valores de hello que escribió en el archivo web.config. Asegúrese de que los nombres de Hola se Hola igual.

![Configuración de la aplicación mostrada en el Portal de Azure][1]

## <a name="authenticate-with-a-certificate-instead-of-a-client-secret"></a>Autenticación con un certificado, en lugar de con un secreto de cliente
Es otra manera tooauthenticate una aplicación de Azure AD mediante un identificador de cliente y un certificado en lugar de un identificador de cliente y el secreto del cliente. A continuación se Hola pasos toouse un certificado en una aplicación Web de Azure:

1. Obtener o crear un certificado
2. Asociar Hola certificado a una aplicación de Azure AD
3. Agregar Hola de toouse de aplicación Web de código tooyour certificado
4. Agregar una aplicación Web de tooyour de certificado

**Obtener o crear un certificado** Para nuestros propósito, crearemos un certificado de prueba. Aquí se muestran un par de comandos que puede usar en un símbolo del sistema para desarrolladores toocreate un certificado. Cambiar toowhere de directorio que desea Hola cert archivos creados.  Además, para hello apertura y cierre de la fecha del certificado de hello, usar hello fecha actual más 1 año.

    makecert -sv mykey.pvk -n "cn=KVWebApp" KVWebApp.cer -b 03/07/2017 -e 03/07/2018 -r
    pvk2pfx -pvk mykey.pvk -spc KVWebApp.cer -pfx KVWebApp.pfx -po test123

Tome nota de la fecha de finalización de Hola y la contraseña de Hola de hello .pfx (en este ejemplo: 31/07/2016 y test123). Las necesitará más adelante.

Para más información sobre cómo crear un certificado de prueba, vea [Procedimientos para crear su propio certificado de prueba](https://msdn.microsoft.com/library/ff699202.aspx)

**Hola asociar certificados con una aplicación de Azure AD** ahora que tiene un certificado, debe tooassociate con una aplicación de Azure AD. Actualmente, Hola Portal de Azure no admite este flujo de trabajo; Esto puede realizarse a través de PowerShell. Ejecute hello siguiendo el certificado de hello tooassoicate de comandos con la aplicación hello Azure AD:

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

Después de ejecutar estos comandos, puede ver la aplicación hello en Azure AD. Al buscar, asegúrese de que seleccionar "Aplicaciones que tiene mi compañía" en lugar de "Aplicaciones que usa mi compañía" en el cuadro de diálogo de búsqueda de Hola.

vea toolearn más información acerca de los objetos de aplicación de Azure AD y objetos ServicePrincipal y [objetos de entidad de servicio y aplicación](../active-directory/active-directory-application-objects.md)

**Agregar Hola de toouse de aplicación Web de código tooyour certificado** ahora agregaremos tooaccess de aplicación Web de código tooyour Hola cert y usarlo para la autenticación.

En primer lugar hay cert de hello tooaccess de código.

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


Tenga en cuenta que Hola StoreLocation es CurrentUser en lugar de LocalMachine. Y que se está proporcionando toohello 'false' Find (método) como estamos usando un certificado de prueba.

A continuación hay código que usa hello CertificateHelper y crea un ClientAssertionCertificate que es necesario para la autenticación.

    public static ClientAssertionCertificate AssertionCert { get; set; }

    public static void GetCert()
    {
        var clientAssertionCertPfx = CertificateHelper.FindCertificateByThumbprint(WebConfigurationManager.AppSettings["thumbprint"]);
        AssertionCert = new ClientAssertionCertificate(WebConfigurationManager.AppSettings["clientid"], clientAssertionCertPfx);
    }


Aquí es Hola nuevo código tooget Hola token de acceso. Esto reemplaza Hola GetToken (método) anterior. Para su comodidad, le hemos dado un nombre diferente.

    public static async Task<string> GetAccessToken(string authority, string resource, string scope)
    {
        var context = new AuthenticationContext(authority, TokenCache.DefaultShared);
        var result = await context.AcquireTokenAsync(resource, AssertionCert);
        return result.AccessToken;
    }

Para facilitar su uso, hemos colocado todo este código en la clase Utils del proyecto de aplicación web.

último cambio de código de Hello es Hola método Application_Start. Primero necesitamos toocall Hola Hola de GetCert() método tooload ClientAssertionCertificate. Y, a continuación, cambiamos el método de devolución de llamada de Hola que se proporciona al crear un nuevo KeyVaultClient. Tenga en cuenta que esto reemplaza el código de hello que hemos tenido anteriormente.

    Utils.GetCert();
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetAccessToken));


**Agregar un certificado tooyour aplicación Web a través del Portal de Azure de Hola** agregar una aplicación Web de tooyour de certificado es un proceso de dos pasos simples. En primer lugar, vaya toohello Portal de Azure y navegue tooyour aplicación Web. En la hoja de configuración de hello para la aplicación Web, haga clic en la entrada de Hola para "los dominios personalizados y SSL". En hello hoja que se abrirá, estarán hello tooupload capaz de certificado que haya creado anteriormente, KVWebApp.pfx, asegúrese de que recordar contraseña Hola Hola pfx.

![Agregar una aplicación Web de certificado tooa Hola Portal de Azure][2]

última cosa que necesite toodo Hello es tooadd una aplicación Web que tiene el sitio Web de nombre de Hola de configuración de la aplicación tooyour\_carga\_certificados y un valor de *. Esto garantizará que se cargan todos los certificados. Si deseara Hola solo tooload certificados en los que se ha cargado, a continuación, puede especificar una lista separada por comas de sus huellas digitales.

vea toolearn más acerca de cómo agregar una aplicación Web, de certificado tooa [con certificados en las aplicaciones de sitios Web de Azure](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/)

**Agregar un almacén de certificados tooKey como un secreto** en lugar de cargar el servicio de aplicación Web de certificado toohello directamente, también puede almacenar en el almacén de claves como un secreto e implementarlo desde allí. Se trata de un proceso de dos pasos que se describe en hello después de la entrada de blog, [implementar certificado Azure la aplicación Web a través del almacén de claves](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)

## <a id="next"></a>Pasos siguientes
Para conocer las referencias de programación, consulte [Referencia de la API de cliente de C# del Almacén de claves](https://msdn.microsoft.com/library/azure/dn903628.aspx).

<!--Image references-->
[1]: ./media/key-vault-use-from-web-application/PortalAppSettings.png
[2]: ./media/key-vault-use-from-web-application/PortalAddCertificate.png
